*Author*: Phuc Lam
*Language*: Vietnamese

# **I. JAM's Evolution from Polkadot**

---

## What is JAM

JAM, viết tắt của **Join-Accumulate Machine**, là một giao thức blockchain hoàn chỉnh và nhất quán, được thiết kế để kết hợp các yếu tố của cả Polkadot và Ethereum. JAM không chỉ là một thiết kế tiềm năng để kế thừa Relay Chain của Polkadot mà còn là một giao thức toàn diện cho môi trường đối tượng không cần quyền toàn cầu, tương tự như môi trường smart contract do Ethereum tiên phong.

Tên gọi "JAM" xuất phát từ CoreJAM, phiên bản đầu tiên và chưa hoàn thiện của giao thức này, được giới thiệu trong một RFC bởi Gavin Wood. CoreJAM lấy tên từ mô hình tính toán collect-refine-join-accumulate, là nền tảng của dịch vụ mà giao thức này hiện thực hóa. Tuy nhiên, JAM đã tiến xa hơn bằng cách cung cấp một giao thức blockchain hoàn chỉnh và nhất quán.

JAM ra đời để giải quyết các hạn chế trong kiến trúc hiện tại của Polkadot, mở đường cho một hệ sinh thái mới với khả năng mở rộng, độ bền vững và tính tương tác tốt hơn, đồng thời vẫn giữ vững tính nhất quán của trạng thái toàn cầu.

JAM sẽ được giới thiệu như một bản nâng cấp toàn diện. Một số yếu tố chính góp phần vào quyết định này:

- Nâng cấp đồng bộ toàn cục cho phép tăng độ chính xác và kiểm soát sau khi nâng cấp điều khó đạt được với phương pháp nâng cấp tuần tự thông thường.
- JAM giúp giảm thiểu các thay đổi nhỏ lẻ và cập nhật thường xuyên, tránh gián đoạn mạng lưới và duy trì sự ổn định của giao thức Polkadot.

## **Key Changes on JAM**

- **Upgradability**:
    - Hiện tại, Polkadot dựa vào các hard forks để thực hiện nâng cấp giao thức, điều này có thể gây gián đoạn và khó khăn trong việc điều phối.
    - JAM giới thiệu một phương pháp liền mạch hơn, cho phép thực hiện các nâng cấp trực tiếp trên chuỗi mà không cần phải dừng mạng lưới. Điều này có nghĩa là giao thức có thể liên tục được cải tiến và thích ứng với các công nghệ mới mà không cần phải trải qua những thay đổi lớn.
- **Services:**
    - Polkadot tập trung vào các Parachains, vốn là các blockchain chuyên biệt với một tập hợp chức năng cố định.
    - JAM giới thiệu một khái niệm mới là Services tương tự như Parachains, vốn linh hoạt và năng động hơn. Các dịch vụ này có thể được triển khai và gỡ bỏ khi cần thiết, mang lại một phạm vi ứng dụng rộng hơn và khả năng phản ứng nhanh hơn đối với các nhu cầu thay đổi.
- **PolkaVM:**
    - Polkadot sử dụng WebAssembly (WASM) để thực thi các hợp đồng thông minh. Dù đảm bảo an toàn, WASM có những hạn chế về tốc độ thực thi, đặc biệt là đối với các tính toán phức tạp.
    - JAM thay thế WASM bằng PolkaVM, một máy ảo có thể tùy chỉnh được thiết kế đặc biệt cho việc thực thi trên mạng lưới blockchain. PolkaVM hứa hẹn mang lại tốc độ thực thi nhanh hơn, bảo mật cao hơn, và linh hoạt hơn trong việc hỗ trợ các ứng dụng đòi hỏi cao hơn.
- **Synchronous Communication:**
    - Giao thức giao tiếp XCM của Polkadot là không đồng bộ, nghĩa là các thông điệp có thể bị trễ hoặc mất.
    - JAM giới thiệu khái niệm ngược lại với Polkadot là giao tiếp đồng bộ, đảm bảo rằng các thông điệp được truyền tải kịp thời và đáng tin cậy. Việc chuyển đổi này giúp cho phép các ứng dụng phức tạp và liên kết chặt chẽ hơn.
- **Security:**
    - PolkaVM, với thiết kế tùy chỉnh và tập trung vào tối ưu hóa dành riêng cho blockchain, được kỳ vọng sẽ tăng cường bảo mật so với WASM.

---

# **II. JAM Architecture: Breaking it Down**

## **Core Components**

Core Components là những khối xây dựng nền tảng của kiến trúc JAM, bao gồm Relay Chain, Services, PolkaVM và Synchronous Communication. Những yếu tố này tạo nên nền tảng cho chức năng và hiệu suất được cải thiện của JAM so với Polkadot.

### **1. Consensus Mechanisms**

JAM chain sử dụng sự kết hợp giữa hai cơ chế đồng thuận là Safrole và Grandpa để quản lý cả việc tạo và hoàn thiện các block trong hệ sinh thái. Safrole đảm bảo rằng các khối được sản xuất một cách có trật tự, trong khi Grandpa hoàn thiện chúng, đảm bảo rằng chúng trở thành một phần hoànn thiện và hiện hữu trong lịch sử của block chain.

Giờ hãy tìm hiểu thêm một ít về 2 cơ chế đồng thuận là **Safrole và Grandpa**

- Safrole Protocol
    - **Mục đích**: Safrole quản lý quá trình sản xuất khối. Nó kiểm soát cách các khối được tạo ra và ngăn chặn các nhánh (fork) bằng cách giới hạn các tác giả khối tiềm năng trong bất kỳ khoảng thời gian sáu giây nào chỉ còn một người giữ khóa xác thực.
    - Tạo khối: Safrole được thiết kế để đảm bảo rằng chỉ có một khối được sản xuất mỗi khoảng thời gian, giúp giảm thiểu khả năng nhiều khối (fork) được sản xuất đồng thời.

- Grandpa Finality
    - **Mục đích**: Grandpa chịu trách nhiệm cho việc hoàn tất các khối. Nó đảm bảo rằng một khi một khối được thêm vào blockchain, nó sẽ vĩnh viễn là một phần của lịch sử blockchain.
    - Finality Protocol: Cơ chế này cung cấp mức độ tin cậy cao rằng một khối sẽ không bị đảo ngược, điều này rất quan trọng cho sự an toàn và độ tin cậy của blockchain.

### **2. Services**

Dịch vụ JAM được chia thành ba điểm truy cập riêng biệt, mỗi điểm truy cập chịu trách nhiệm cho một loại hoạt động cụ thể:

- **Refine:** Đây là hàm thực hiện các tính toán hầu như không thay đổi trạng thái (stateless). Hàm này định nghĩa quá trình biến đổi cho rollup (rollup) của một dịch vụ cụ thể. Refine xử lý các work item (work item), là đầu vào của dịch vụ, và tạo ra work result (work result), là đầu ra của dịch vụ đó. Refine thường được thực hiện ngoài chuỗi (off-chain), trong môi trường "trong lõi" (in-core).
- **Accumulate:** Đây là hàm nhận đầu ra từ Refine (work result) và tích hợp nó vào trạng thái tổng thể của dịch vụ. Accumulate tích hợp các work report (work report), là kết quả của nhiều work item, vào trạng thái dịch vụ. Quá trình này thường được thực hiện trên chuỗi (on-chain).
- **OnTransfer:** Hàm này xử lý thông tin đến từ các dịch vụ khác. Hàm này xử lý các giao dịch chuyển token giữa các dịch vụ khác nhau, đảm bảo rằng số dư chính xác được duy trì. Hàm này cũng thường được thực hiện trên chuỗi (on-chain).

### **4. PolkaVM**

Polkadot Virtual Machine (PVM) là một máy ảo được thiết kế cho mạng lưới Polkadot. Nó là một phần quan trọng trong JAM (Join-Accumulate Machine), một giao thức blockchain được Gavin Wood đề xuất và được sử dụng để thực hiện các smart contract trên mạng lưới Polkadot.

PVM dựa trên kiến trúc tập lệnh RISC-V (`Instruction Set Architecture`), nổi tiếng với sự đơn giản và đa năng. RISC-V ISA mang lại nhiều lợi ích:

- **Sandboxing**: PVM có khả năng cô lập, đảm bảo tính bảo mật cao trong quá trình thực thi.
- **Deterministic Execution**: PVM đảm bảo tính xác định trong quá trình thực thi, đồng nghĩa với việc kết quả sẽ luôn giống nhau với cùng một tập đầu vào.
- **Performance Optimization**: PVM tối ưu hóa hiệu suất với khả năng chuyển đổi dễ dàng giữa các định dạng phần cứng phổ biến như x86, x64 và ARM. Nó cũng được hỗ trợ tốt bởi các công cụ như LLVM.

Bản thân PVM thể hiện sự đơn giản và bảo mật, có thể được cô lập (sandboxable) và cung cấp nhiều đảm bảo về việc thực thi. Nó có tính xác định, nhạy cảm với sự đồng thuận và thân thiện với việc tính toán chi phí (metering). Không giống như các máy ảo khác, PVM không phức tạp và không có nhiều quan điểm thiên vị.

WASM thường gặp khó khăn trong quản lý ngăn xếp và xử lý điểm ngắt, nhưng RISC-V giải quyết vấn đề này bằng cách đặt ngăn xếp trong bộ nhớ, giúp xử lý tự nhiên mà không phức tạp thêm. PVM cũng cho tốc độ thực thi xuất sắc trên phần cứng thông thường như X64 và ARM, đồng thời cung cấp lợi thế về chi phí so với WASM.

Việc tích hợp các điểm ngắt được hỗ trợ bởi RISC-V dự kiến sẽ thiết lập tiêu chuẩn mới cho mã hóa có khả năng mở rộng trên các nền tảng đa lõi như JAM, một xu hướng cần thiết để mở rộng các thuật toán blockchain và đồng thuận trong tương lai.

### **5. Synchronous Communication**

Hàm `onTransfer` trong hệ thống JAM cũng là một hàm thay đổi trạng thái (stateful), cho phép nó sửa đổi trạng thái của các `Services`. Hàm này có khả năng kiểm tra trạng thái của các dịch vụ khác và thực hiện thay đổi đối với trạng thái của chính nó. Chức năng này tạo điều kiện thuận lợi cho việc giao tiếp giữa các dịch vụ, mặc dù theo cách thức bất đồng bộ (asynchronous).

Không giống như nhiều Smart Contract khác, nơi các tương tác diễn ra đồng bộ (synchronously), trong JAM, các thành phần như Smart Contract hoặc dịch vụ tương tác với nhau theo cách bất đồng bộ (asynchronously). Messages và Token được gửi đi, và tại một thời điểm sau đó trong cùng một chu kỳ thực thi khoảng 6 giây, phía Services nhận sẽ xử lý chúng.

- Không có phản hồi trực tiếp từ dịch vụ nhận; nếu cần phản hồi, dịch vụ gửi phải khởi tạo một giao dịch mới hoặc thay đổi trạng thái của mình sao cho dịch vụ nhận có thể hiểu và xử lý sau này.
    - Điều này có nghĩa là hệ thống không cung cấp phản hồi ngay lập tức.
    - Nếu dịch vụ gửi cần phản hồi, nó phải thực hiện các hành động bổ sung, chẳng hạn như:
        - Tạo giao dịch mới.
        - Điều chỉnh trạng thái để dịch vụ nhận có thể nhận biết và đáp ứng trong lần xử lý tiếp theo.

**Ví dụ đơn giản:**

- **Smart Contract** giống như khi bạn hỏi ai đó một câu hỏi và họ trả lời ngay lập tức. Đó là cách thông thường mà các Smart Contract khác hoạt động, chúng trả lời ngay lập tức.
- Nhưng với **JAM**, khi bạn gửi một câu hỏi (giống như gửi một thông điệp hoặc một token), người nhận không trả lời ngay lập tức. Thay vào đó, họ nhận câu hỏi của bạn, suy nghĩ một chút (trong khoảng 6 giây), và sau đó mới trả lời.
- Và nếu bạn muốn họ trả lời câu hỏi của bạn sau khi họ suy nghĩ xong, bạn phải làm một trong hai việc:
    - **Gửi một câu hỏi khác** để nhắc họ trả lời.
    - **Thay đổi cách bạn nói chuyện** để họ hiểu rằng bạn đang cần câu trả lời.

Cả hàm `Accumulate` và `onTransfer` đều được thiết kế để thực hiện song song (parallel), cho phép tích lũy và chuyển giao của các dịch vụ khác nhau diễn ra đồng thời. Thiết kế này mở ra khả năng nâng cấp trong tương lai, chẳng hạn như phân bổ nhiều hơn 10 mili giây gas đầu vào hiện tại. Về lý thuyết, một lõi phụ (secondary core) có thể được sử dụng để thực hiện một số tích lũy, cung cấp cho chúng nhiều gas hơn để sử dụng.

**Kết nối đồng bộ** (Synchronous Communication) có thể được tích hợp vào JAM trong các trường hợp cụ thể, nhưng phần lớn hệ thống hoạt động dựa trên cơ chế bất đồng bộ để phù hợp với các yêu cầu về hiệu suất và tính mở rộng.

Tham khảo thêm tại: [On Transfer Function](https://wiki.polkadot.network/docs/learn-jam-chain#on-transfer-function)

---

# III. **Networking**

Jam được thiết kế như một hệ thống phân tán, nơi nhiều node kết nối và giao tiếp với nhau qua một mạng lưới. Mạng lưới này đóng vai trò quan trọng trong việc đảm bảo sự đồng bộ hóa trạng thái và hoạt động hiệu quả của hệ thống.

- QUIC protocol : Mạng lưới của JAM sử dụng [QUIC-Protocol](https://en.wikipedia.org/wiki/QUIC). Điều này cho phép kết nối các node với nhau giữa một số lượng lớn các validator. Thực tế, tất cả hơn 1.000 validator trên Polkadot có thể có kết nối liên tục với nhau mà không gặp vấn đề tiềm ẩn với các socket.
- **Gossip**: Trong JAM Chain, gossip được hạn chế được sử dụng vì nó không không quá cần thiết. JAM không xử lý các giao dịch, do đó không cần phải truyền tải thông tin rộng rãi như trong Polkadot. Thay vào đó, JAM sử dụng giao thức QUIC để kết nối trực tiếp điểm-điểm giữa các validator. Điều này giúp tất cả hơn 1.000 validator trên Polkadot có thể kết nối liên tục với nhau mà không gặp vấn đề với các socket.

---

# **IV. Advantages and Potential of JAM**

JAM, với kiến trúc sáng tạo và các tính năng bảo mật tiên tiến, không chỉ mang lại khả năng mở rộng và hiệu suất vượt trội mà còn mở ra những tiềm năng mới cho toàn bộ hệ sinh thái blockchain, vượt xa phạm vi DeFi. Với thiết kế linh hoạt và tập trung vào tính toàn vẹn và nhất quán của trạng thái toàn cầu, JAM hứa hẹn sẽ trở thành một nền tảng mạnh mẽ cho các ứng dụng Web3 và beyond.

**Điểm mạnh của JAM:**

- **Khả năng mở rộng vượt trội (Superior Scalability):** JAM cho phép thực hiện các tính toán phức tạp với lượng dữ liệu lớn trong môi trường đồng thuận bảo mật mà không làm giảm tính nhất quán của hệ thống. Cấu trúc phân mảnh linh hoạt của JAM giúp tránh tình trạng phân mảnh trạng thái và duy trì tính toàn vẹn của dữ liệu.
- **Hiệu suất cao (High Performance):** Nhờ vào PolkaVM và các cơ chế đồng thuận tiên tiến như Safrole và Grandpa, JAM đạt được hiệu suất xử lý cao hơn so với các mô hình blockchain truyền thống. Kiến trúc đa lõi (parallelism) giúp tối ưu hóa hiệu suất và giảm thiểu độ trễ.
- **Bảo mật nâng cao (Enhanced Security):** JAM áp dụng các cơ chế bảo mật tiên tiến, như sandboxing trong PolkaVM và sự kết hợp của các giao thức đồng thuận Safrole và Grandpa, đảm bảo rằng hệ thống luôn hoạt động trong môi trường an toàn và đáng tin cậy.
- **Khả năng kết hợp và tương tác (Interoperability and Composability):** JAM hỗ trợ tích hợp linh hoạt với nhiều dịch vụ và ứng dụng khác nhau, cho phép tạo ra các ứng dụng phức tạp và tương tác cao. Khả năng này giúp JAM trở thành một nền tảng lý tưởng cho việc phát triển các dịch vụ đa dạng trong hệ sinh thái Web3.
- **Tương tác linh hoạt giữa các dịch vụ (Flexible Service Interaction):** JAM không chỉ hỗ trợ giao tiếp đồng bộ mà còn cho phép giao tiếp bất đồng bộ giữa các dịch vụ, tạo ra một môi trường linh hoạt và hiệu quả cho các ứng dụng cần phản hồi nhanh và chính xác.

**Tiềm năng của JAM:**

- **Thúc đẩy sự phát triển của Web3:** JAM có tiềm năng trở thành nền tảng nền tảng mạnh mẽ cho việc triển khai các ứng dụng Web3 phức tạp, không chỉ trong lĩnh vực DeFi mà còn trong nhiều lĩnh vực khác như quản lý tài sản số, trò chơi blockchain, và các ứng dụng doanh nghiệp.
- **Tạo dựng một hệ sinh thái blockchain mạnh mẽ:** Với khả năng tương tác và mở rộng, JAM có thể đóng vai trò quan trọng trong việc xác thực các parachain và thúc đẩy sự phát triển của toàn bộ hệ sinh thái Polkadot, tạo ra một mạng lưới blockchain linh hoạt, đa dạng và bền vững.

---

# **V. Challenges and Future Directions**

JAM là một bước tiến lớn trong kiến trúc blockchain, nhưng đi kèm với đó là những thách thức kỹ thuật và nhu cầu nghiên cứu thêm để phát huy hết tiềm năng của nó. Việc đánh giá và cải thiện các giới hạn lý thuyết và thực nghiệm của JAM là cần thiết để đảm bảo tính khả thi và hiệu quả trong các môi trường ứng dụng thực tế.

**Thách thức:**

- **Tối ưu hóa khả năng mở rộng và hiệu suất thực tế:** Dù JAM hứa hẹn khả năng mở rộng vượt trội, nhưng vẫn cần có thêm nghiên cứu thực nghiệm để xác định cách những giới hạn lý thuyết này chuyển thành hiệu suất thực tế. Điều này bao gồm việc thực hiện các bài kiểm tra hiệu suất chi tiết và phân tích chi phí so với các giao thức hiện có.
- **Cân bằng giữa phân mảnh và tính nhất quán:** Một trong những thách thức lớn của JAM là duy trì tính toàn vẹn và nhất quán của trạng thái toàn cầu trong khi vẫn đảm bảo khả năng mở rộng và hiệu suất. Điều này đòi hỏi sự tinh chỉnh liên tục trong các cơ chế đồng thuận và giao tiếp giữa các dịch vụ.
- **An ninh và bảo mật:** Bảo vệ mạng JAM trước các mối đe dọa mới nổi là một ưu tiên hàng đầu. Cần phải liên tục kiểm tra và cải thiện các cơ chế bảo mật, như sandboxing trong PolkaVM và sự kết hợp giữa các giao thức Safrole và Grandpa, để đảm bảo rằng JAM vẫn là một nền tảng an toàn và đáng tin cậy.
- **Quản lý tài nguyên và khả năng mở rộng:** Việc quản lý tài nguyên hiệu quả, đặc biệt là trong môi trường dịch vụ phân mảnh của JAM, đặt ra những thách thức về tối ưu hóa phân bổ tài nguyên và khả năng xử lý song song. Điều này có thể bao gồm việc phát triển các phương pháp mới để dự trữ và sử dụng hiệu quả hơn dung lượng tính toán trong quá trình tích lũy.

**Định hướng tương lai:**

- **Nghiên cứu thực nghiệm và tối ưu hóa:** JAM cần tiếp tục được nghiên cứu thực nghiệm để hiểu rõ hơn về các giới hạn hiệu suất và tối ưu hóa các cơ chế hiện có. Ngoài ra, việc so sánh và phân tích chi phí với các giao thức khác sẽ giúp định hình những cải tiến cần thiết trong tương lai.
- **Tích hợp các khả năng tính toán mới:** Định hướng tương lai của JAM bao gồm việc tích hợp các tính năng mới như Merklization vào định dạng Gói Công Việc để cải thiện hiệu quả xử lý và tính bảo mật. Ngoài ra, phát triển các phương pháp giao tiếp đồng bộ và bất đồng bộ tiên tiến hơn sẽ giúp nâng cao khả năng tương tác và tối ưu hóa hiệu suất toàn hệ thống.
- **Cải thiện trải nghiệm người dùng và nhà phát triển:** Một trong những mục tiêu dài hạn của JAM là làm cho giao thức này dễ sử dụng hơn cho cả người dùng và nhà phát triển. Điều này có thể bao gồm việc phát triển thêm các công cụ hỗ trợ và tài liệu hướng dẫn chi tiết, cũng như tối ưu hóa giao diện lập trình để đơn giản hóa quá trình phát triển ứng dụng trên nền tảng JAM.

---

# VI. R**esilience on JAM**

Khả năng phục hồi (Resilience) là một yếu tố quan trọng đối với bất kỳ hệ thống blockchain nào, đặc biệt là trong môi trường phi tập trung của Web3. JAM được thiết kế để đạt được khả năng phục hồi cao thông qua việc kết hợp một số cơ chế bảo mật và khả năng phục hồi độc đáo.

**1. Bảo mật mạng lưới:**

- **Mã hóa:** JAM sử dụng mã hóa để bảo mật các giao tiếp giữa các node, giúp bảo vệ mạng lưới khỏi các cuộc tấn công mạng lưới như tấn công từ chối dịch vụ (DoS) và tấn công người trong cuộc (MITM).
- **Entropy:** Cơ chế đồng thuận Safrole tạo ra một nhóm entropy có thể được sử dụng bởi các phần khác của giao thức, giúp tăng cường bảo mật và độ ngẫu nhiên cho hệ thống.

**2. Khả năng phục hồi của chuỗi khối:**

- **Cơ chế đồng thuận:** JAM sử dụng một cơ chế đồng thuận kết hợp giữa Safrole và Grandpa, giúp đảm bảo rằng các khối được thêm vào chuỗi một cách an toàn và không thể bị đảo ngược.
    - **Safrole:** Safrole kiểm soát quá trình sản xuất khối, giúp giảm thiểu khả năng nhiều khối (nhánh) được tạo ra đồng thời. Nó cũng tạo ra một nhóm entropy có thể được sử dụng bởi các phần khác của giao thức.
    - **Grandpa:** Grandpa chịu trách nhiệm cho việc hoàn thiện các khối, đảm bảo rằng một khi một khối được thêm vào blockchain, nó sẽ trở thành một phần vĩnh viễn của lịch sử blockchain.
- **Mã hóa kinh tế:** JAM dựa vào các cơ chế mã hóa kinh tế để khuyến khích các node xác thực hành động trung thực và trừng phạt các hành động bất chính.

**3. Bảo mật dữ liệu:**

- **Merklization:** JAM sử dụng Merklization để tạo ra một bản sao lưu của dữ liệu trạng thái, giúp bảo vệ dữ liệu khỏi bị mất mát hoặc bị sửa đổi.
- **Kiểm tra tính khả dụng:** Cơ chế kiểm tra tính khả dụng của dữ liệu (Data Availability) đảm bảo rằng dữ liệu được phân phối một cách an toàn và có thể được truy cập bởi tất cả các node.

**4. Khả năng phục hồi của hệ thống:**

- **Jam được thiết kế để hoạt động hiệu quả ngay cả khi có sự cố xảy ra với một số node trong mạng lưới.** Cơ chế đồng thuận của Jam đảm bảo rằng chuỗi khối vẫn có thể hoạt động ngay cả khi một số node bị lỗi hoặc bị tấn công.
- **Jam có khả năng phục hồi cao (Resilience) bởi vì nó được thiết kế để chống lại các cuộc tấn công và lỗi kỹ thuật.** Các cơ chế bảo mật và khả năng phục hồi của Jam giúp đảm bảo rằng hệ thống có thể hoạt động ổn định và đáng tin cậy trong môi trường phi tập trung.

**5. Khả năng phục hồi của các dịch vụ:**

- **JAM được thiết kế để đảm bảo rằng các dịch vụ vẫn có thể hoạt động hiệu quả ngay cả khi có sự cố xảy ra với một số node trong mạng lưới.** Cơ chế đồng thuận của Jam đảm bảo rằng chuỗi khối vẫn có thể hoạt động ngay cả khi một số node bị lỗi hoặc bị tấn công.
- **JAM có khả năng phục hồi cao (Resilience) bởi vì nó được thiết kế để chống lại các cuộc tấn công và lỗi kỹ thuật.** Các cơ chế bảo mật và khả năng phục hồi của Jam giúp đảm bảo rằng hệ thống có thể hoạt động ổn định và đáng tin cậy trong môi trường phi tập trung.

**6. Khả năng phục hồi của các validator:**

- **JAM được thiết kế để đảm bảo rằng các validator vẫn có thể hoạt động hiệu quả ngay cả khi có sự cố xảy ra với một số node trong mạng lưới.** Cơ chế đồng thuận của Jam đảm bảo rằng chuỗi khối vẫn có thể hoạt động ngay cả khi một số node bị lỗi hoặc bị tấn công.
- **JAM có khả năng phục hồi cao (Resilience) bởi vì nó được thiết kế để chống lại các cuộc tấn công và lỗi kỹ thuật.** Các cơ chế bảo mật và khả năng phục hồi của Jam giúp đảm bảo rằng hệ thống có thể hoạt động ổn định và đáng tin cậy trong môi trường phi tập trung.