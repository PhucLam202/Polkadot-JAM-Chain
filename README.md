*Author*: Phuc Lam

*Language*: Vietnamese

# **I. JAM's Evolution from Polkadot**

---

## What is JAM ?

JAM, viết tắt của **Join-Accumulate Machine**, là một giao thức blockchain hoàn chỉnh và nhất quán, được thiết kế để kết hợp các yếu tố của cả Polkadot và Ethereum. JAM không chỉ là một thiết kế tiềm năng để kế thừa Relay Chain của Polkadot mà còn là một giao thức toàn diện cho môi trường đối tượng không cần quyền toàn cầu.

Tên gọi "JAM" xuất phát từ CoreJAM, phiên bản đầu tiên và chưa hoàn thiện của giao thức này, được giới thiệu trong một RFC bởi Gavin Wood. CoreJAM lấy tên từ mô hình tính toán Collect-Refine-Join-Accumulate, là nền tảng của dịch vụ mà giao thức này hiện thực hóa. Tuy nhiên, JAM đã tiến xa hơn bằng cách cung cấp một giao thức blockchain hoàn chỉnh và nhất quán.

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
    - Giao thức giao tiếp XCM của Polkadot giao tiếp một cách bất đồng bộ (asynchronously) với nhau, điều đó có nghĩa là các thông điệp có thể bị trễ hoặc mất trong quá trình truyền tải.
    - JAM giới thiệu khái niệm ngược lại với Polkadot là giao tiếp đồng bộ (synchronously), điều đó đảm bảo rằng các thông điệp được truyền tải kịp thời với độ tin cậy cao. Việc chuyển đổi này giúp cho phép các ứng dụng phức tạp sẽ có được tính liên kết chặt chẽ hơn so với XCM.
- **Security:**
    - PolkaVM, với thiết kế tùy chỉnh và tập trung vào tối ưu hóa dành riêng cho blockchain, được kỳ vọng sẽ tăng cường bảo mật hơn so với WASM truyền thống.

---

# II. WASM

## What is WebAssembly?

**WebAssembly** là một tiêu chuẩn mở, được thiết kế chặt chẽ và có hệ sinh thái mạnh mẽ Wasm là thành quả của sự hợp tác giữa những ông lớn công nghệ sở hữu trình duyệt phổ biến nhất hiện nay gồm Microsoft, Apple, Google, Mozilla,…, với nhiều máy ảo chất lượng cao sẵn có, như `Wasmtime`, `Wasmer`, `Wasmi`, `WAVM`, `wazero`, `Wasm3`, và `WasmEdge`. Những máy ảo này giúp Wasm trở thành nền tảng phổ biến và hỗ trợ thực thi mã trên nhiều nền tảng với hiệu suất cao. Đặc biệt, Wasm được viết bằng ngôn ngữ Rust bởi đội ngũ kỹ sư hàng đầu trong lĩnh vực máy ảo, mang đến độ an toàn và hiệu suất cao nhờ vào việc:

- **Biên dịch mã Wasm thành mã máy** để thực thi nhanh chóng.
- **Độ bảo mật cao** do được kiểm thử và `fuzzing` kỹ lưỡng.
- **Thời gian biên dịch nhanh** và khả năng phát triển nhanh chóng nhờ vào hệ thống công cụ và thư viện của Rust.

## How WASM Work?

Với WebAssembly, mã nguồn (source code) sẽ được viết bằng các ngôn ngữ lập trình bậc cao như C/C++, Rust,… sau đó biên dịch về định dạng nhị phân (.wasm). Những file này sẽ được nạp vào trình duyệt rồi nhờ các JavaScript Engine biên dịch tạo ra mã máy để thực thi.

![WebAssembly-2.jpg](./image/WebAssembly-2.jpg)

## The Limitations of WebAssembly in Polkadot

- **Không đảm bảo tính xác định 100%**: Wasm không thể đảm bảo hoàn toàn tính **determinism** do **guest stack** và **host stack** được chia sẻ, gây ra các khác biệt nhỏ trong kết quả tính toán giữa các nút. Đây là một bất lợi lớn cho các hệ thống yêu cầu tính nhất quán tuyệt đối như Polkadot.
- **Không có giới hạn số lượng hàm lồng nhau**: Wasm cho phép gọi hàm đệ quy và lồng nhau không giới hạn, có thể dẫn đến tình trạng quá tải ngăn xếp và làm giảm hiệu suất khi triển khai trên quy mô lớn.
- **Thời gian biên dịch không đảm bảo O(n)**: Quá trình biên dịch mã trong Wasm không đảm bảo tốc độ tuyến tính, khiến quá trình biên dịch có thể bị chậm. Trong hệ thống Polkadot, PVF cần pre-check để xác minh mã có thể được chấp nhận, nhưng điều này không luôn luôn đảm bảo được tốc độ mong muốn.
- **Thiếu các tính năng cần thiết**:
    - **Suspend + Resume** (tạm dừng và tiếp tục): Wasm thiếu hỗ trợ cho việc [**suspend + resume**](https://github.com/WebAssembly/design/issues/1294) của các chương trình, điều này quan trọng trong các ứng dụng phức tạp cần kiểm soát luồng thực thi.
    - **Gas Metering**: Wasm thiếu hệ thống tính phí theo chuẩn cho các ứng dụng blockchain, điều này gây khó khăn trong việc kiểm soát và hạn chế mức tiêu thụ tài nguyên.
    - **Dynamic Page Fault Handling**: Thiếu khả năng xử lý **dynamic guest page fault** có thể gây ảnh hưởng đến khả năng mở rộng và triển khai trong môi trường blockchain với yêu cầu cao về tính năng động của tài nguyên.

## Solution for Polkadot

Để đáp ứng các nhu cầu đặc thù của blockchain, Polkadot cần một kiến trúc tập lệnh (ISA) thay thế, với các đặc tính lý tưởng yều câu sau:

- Thiết kế đơn giản, dễ triển khai.
- Tiêu chuẩn ổn định và duy trì lâu dài.
- Được hỗ trợ rộng rãi và có công cụ phát triển tốt.
- Không ép buộc các tính năng không cần thiết, nhằm tập trung tối đa vào hiệu suất và tính bảo mật.

---

# **III. RISC-V**

Trước khi đi vào các phần chính thì ta nên điểm qua một ít về khái niệm về RISC-V. Đây là một kiến trúc lõi có ảnh hưởng trực tiếp đến PVM sẽ được đề cập bên dưới 

## **What is RISC-V ?**

Trước khi đi vào các phần chính, hãy cùng xem qua RISC-V, một kiến trúc quan trọng dựa trên nguyên tắc của kiến trúc tập lệnh rút gọn (RISC), với đặc tính mã nguồn mở, tự do sử dụng và tùy chỉnh. Điều này khác biệt so với các kiến trúc tập lệnh như x86 hoặc ARM, vốn được kiểm soát bởi các nhà cung cấp cụ thể, trong khi [RISC-V](https://www.synopsys.com/glossary/what-is-risc-v.html) cho phép mọi người tự do đóng góp và phát triển.

### Key Features of RISC-V

- **Modularity (Tính mô-đun):** RISC-V có một tập lệnh cơ sở nhỏ gọn và hiệu quả, cùng khả năng mở rộng linh hoạt. Điều này cho phép các hệ thống có thể tùy chỉnh tập lệnh thông qua các phần mở rộng như **Compressed Instructions (C)** và **Atomic Instructions (A)**, giúp tối ưu hóa hiệu suất và nâng cao tính bảo mật tùy theo nhu cầu cụ thể của từng ứng dụng.
    - **Compressed Instructions (C):** Phần mở rộng này cho phép mã lệnh được nén lại, giảm kích thước của chương trình và tiết kiệm bộ nhớ. Tập lệnh nén giúp thay thế các lệnh dài 32-bit bằng các lệnh ngắn hơn 16-bit, nhờ đó giảm kích thước bộ nhớ yêu cầu và cải thiện hiệu suất sử dụng bộ nhớ đệm.
        - ⇒ Tham khảo thêm: [Compressed Instructions](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2016/EECS-2016-118.pdf) (trang 89)
    - **Atomic Instructions (A):** Phần mở rộng này hỗ trợ các thao tác nguyên tử, rất hữu ích trong việc quản lý truy cập đồng thời vào bộ nhớ trên các hệ thống đa nhân, giúp cải thiện tính nhất quán và hiệu quả trong các thao tác đòi hỏi tính đồng thời cao.
        - ⇒ Tham khảo thêm: [Atomic Instructions](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2016/EECS-2016-118.pdf) (trang 45)
- **Simplicity (Tính đơn giản):** Sự đơn giản trong thiết kế của RISC-V mang lại nhiều lợi ích cho các hệ thống ứng dụng, giúp giảm chi phí và thời gian phát triển phần cứng. Đặc điểm này còn cho phép các kỹ sư xác minh chính xác tính đúng đắn của hệ thống, tăng cường độ tin cậy và an toàn cho các ứng dụng.
- **Extensibility (Khả năng mở rộng):** Khả năng mở rộng của RISC-V giúp nó dễ dàng thích ứng với các thay đổi công nghệ trong tương lai. Các phần mở rộng được chuẩn hóa để đảm bảo tính tương thích và tránh tình trạng phân mảnh, giúp các hệ thống triển khai dựa trên RISC-V dễ dàng nâng cấp và tích hợp tính năng mới. Tính mở và minh bạch của quy trình này khuyến khích sự tham gia của cộng đồng, thúc đẩy sự đổi mới liên tục.
- **Open Standard (Tiêu chuẩn mở):** Tính mở của RISC-V thúc đẩy sự hợp tác và ngăn chặn sự phụ thuộc vào nhà cung cấp, tạo ra một hệ sinh thái phát triển phần cứng và phần mềm phong phú, năng động và đa dạng.

---

# IV. Comparison between PolkaVM and WASM

**Tốc độ Biên Dịch**: PolkaVM được tuyên bố sẽ nhanh hơn 300 lần so với Wasmtime, điều này giúp tối ưu hóa thông lượng trong blockchain, trong khi WASM có tốc độ biên dịch chậm hơn, có thể gây hạn chế trong quá trình phát triển nhanh.

**Bytecode**:  PolkaVM sử dụng bytecode tùy chỉnh, được thiết kế cho tốc độ và hiệu quả, giúp chuyển đổi lệnh 1-đối-1 thành mã gốc, tối ưu hóa cho blockchain. WASM không hoàn toàn phù hợp với kịch bản này và có thể dẫn đến tiêu tốn tài nguyên.

**Lazy Execution**: PolkaVM hỗ trợ thực thi lười (lazy execution), giúp giảm tải tài nguyên. WASM thường yêu cầu thực thi tất cả mã cần thiết ngay từ đầu, có thể kém hiệu quả trong môi trường tài nguyên giới hạn.

**Hiệu Suất & Xác Định**: PolkaVM đạt tốc độ thực thi tương đương với Wasmtime và nhanh hơn trong biên dịch gấp 320 lần, đồng thời đảm bảo tính xác định 100%, rất quan trọng để duy trì nhất quán giữa các nút trong blockchain.

**Bảo mật**: PVM cung cấp môi trường sandboxing tiên tiến với các biện pháp bảo mật chặt chẽ (như seccomp), đảm bảo tính cách ly cao hơn cho các ứng dụng phân tán so với WASM.

**Ngôn Ngữ**: PolkaVM hỗ trợ các ngôn ngữ C, C++, và Rust, mở rộng tính linh hoạt so với các ngôn ngữ tương thích WASM truyền thống, giúp dễ dàng tích hợp vào hệ sinh thái blockchain hiện có.

**Tương Thích Với Substrate:**
PolkaVM được thiết kế để hoạt động hiệu quả trên Substrate và chạy Rococo trên mạng thử nghiệm của Polkadot. Trong khi WASM cũng có mặt trong Substrate, PolkaVM tối ưu hóa cho nhu cầu blockchain cụ thể của Polkadot hơn.

| **Tính năng** | **WASM** | **RISC-V** | **PVM (PolkaVM)** |
| --- | --- | --- | --- |
| Kiến trúc | Stack-based | Register-based | Register-based (dựa trên RISC-V) |
| Mục đích | Chung, web, blockchain | Chung, nhúng, IoT, blockchain | Đặc biệt dành cho Substrate (Polkadot) |
| Tốc độ Biên dịch | Thường được coi là chấp nhận được trong thực tế, nhưng vẫn chậm hơn PVM

VD: thời gian biên dịch WASM là 10s  | N/A (không áp dụng cho kiến trúc do RISC-V phụ thuộc vào kiến trúc phần cứng) | Nhanh hơn WASM đáng kể (theo Document được đề ra của Gavin Wood , có thể lên đến 300 lần)

VD: thời gian biên dịch **PVM** là 0.5s  |
| Hiệu suất | Tốt (gần native code) | Cao (trong lý thuyết, phụ thuộc vào phương thức triển khai) | Tương đương Wasmtime (một runtime WASM), nhanh hơn WASM trong biên dịch |
| Tính Xác Định | Hướng tới, nhưng có thể gặp thách thức (floating-point, thư viện hệ thống, bộ nhớ dùng chung) | Cao (phụ thuộc vào triển khai và mã nguồn) | Cao |
| Bảo mật | Sanbox | Cơ chế bảo mật phần cứng (tùy thuộc) | Enhanced Sanbox (seccomp, tiến trình riêng) |
| Ngôn ngữ | C/C++, Rust, AssemblyScript, Go, C#, Swift, D, Zig, Kotlin/Native, và nhiều ngôn ngữ khác | C/C++, Rust, Go, Python, Java, và nhiều ngôn ngữ khác | C, C++, Rust |
| Tích hợp Substrate | Có, nhưng không tối ưu | N/A | Tối ưu, đang trong quá trình thực thi và thử nghiệm |
| Độ tăng trưởng | Cao, được sử dụng một cách rộng rãi (hỗ trợ bởi nhiều trình duyệt, công cụ, cộng đồng lớn) | Cao | Thử nghiệm, đang trong quá trình phát triển |
| Ưu điểm | Hỗ trợ rộng rãi, cộng đồng lớn, nhiều công cụ và thư viện | Hiệu suất, linh hoạt | Tốc độ biên dịch cực nhanh, bảo mật, tối ưu cho Substrate |
| Nhược điểm | Hiệu suất hạn chế trong Substrate, tiềm ẩn vấn đề về tính xác định | Phụ thuộc vào triển khai cụ thể | Đang phát triển, chưa được kiểm chứng rộng rãi, ít ngôn ngữ được hỗ trợ hơn |

---

# **V. JAM Architecture: Breaking it Down**

## **Core Components**

Core Components là những khối xây dựng nền tảng của kiến trúc JAM, bao gồm Relay Chain, Services, PolkaVM và Synchronous Communication. Những yếu tố này tạo nên nền tảng cho chức năng và hiệu suất được cải thiện của JAM so với Polkadot.

### **1. Consensus Mechanisms**

JAM chain sử dụng sự kết hợp giữa hai cơ chế đồng thuận là Safrole và Grandpa để quản lý cả việc tạo và hoàn thiện các block trong hệ sinh thái. Safrole đảm bảo rằng các khối được sản xuất một cách có trật tự, trong khi Grandpa hoàn thiện chúng, đảm bảo rằng chúng trở thành một phần hoàn thiện và hiện hữu trong lịch sử của blockchain.

### **Safrole Protocol**

- **Mục đích**: Safrole quản lý quá trình sản xuất khối. Nó kiểm soát cách các khối được tạo ra và ngăn chặn các nhánh (fork) bằng cách giới hạn các tác giả khối tiềm năng trong bất kỳ khoảng thời gian sáu giây nào chỉ còn một người giữ khóa xác thực.
- **Tạo khối**: Safrole được thiết kế để đảm bảo rằng chỉ có một khối được sản xuất mỗi khoảng thời gian, giúp giảm thiểu khả năng nhiều khối (fork) được sản xuất đồng thời.

      ⇒ Tham khảo thêm: [Safrole](https://wiki.polkadot.network/docs/learn-safrole)

### **Grandpa Finality**

- **Mục đích**: Grandpa chịu trách nhiệm cho việc hoàn tất các khối. Nó đảm bảo rằng một khi một khối được thêm vào blockchain, nó sẽ vĩnh viễn là một phần của lịch sử blockchain.
- **Finality Protocol**: Cơ chế này cung cấp mức độ tin cậy cao rằng một khối sẽ không bị đảo ngược, điều này rất quan trọng cho sự an toàn và độ tin cậy của blockchain.

      ⇒ Tham khảo thêm: [GRANDPA](https://wiki.polkadot.network/docs/learn-consensus#finality-gadget-grandpa)

### **Hybrid Consensus trong Polkadot**

Polkadot sử dụng cơ chế đồng thuận lai, kết hợp giữa BABE và GRANDPA, để đảm bảo tính nhất quán và an toàn của mạng lưới.

- **BABE (Blind Assignment for Blockchain Extension)**: Là cơ chế sản xuất block, sử dụng hàm ngẫu nhiên có thể xác minh (VRF) để chỉ định các validator cho các slot trong mỗi epoch. Điều này đảm bảo rằng các block được sản xuất liên tục và có tính xác suất.
- **GRANDPA (GHOST-based Recursive Ancestor Deriving Prefix Agreement)**: Là cơ chế hoàn thiện block, cung cấp một cơ chế bỏ phiếu cho các chuỗi block. GRANDPA đảm bảo rằng một khi một block được hoàn thiện, nó sẽ không thể bị đảo ngược, cung cấp tính hoàn thiện có thể chứng minh được.

Cơ chế đồng thuận lai này cho phép Polkadot đạt được cả tính xác suất và tính hoàn thiện có thể chứng minh được, giúp mạng lưới hoạt động hiệu quả và an toàn.

![GRuM9LiaYAA9Fsb.jpg](./image/ReychainHybridConensus.jpg)

⇒ Tham khảo thêm: [Hybrid Consensus](https://x.com/openguildwtf/status/1809203505649037391)

### **2. Services**

Dịch vụ JAM được chia thành nhiều thành phần, mỗi thành phần chịu trách nhiệm cho một hoạt động cụ thể liên quan đến việc xử lý và tích lũy dữ liệu. Các thành phần chính bao gồm:

- **Refine**: Đây là thành phần thực hiện các tính toán không thay đổi trạng thái (stateless). Nhiệm vụ của **Refine** là xử lý các "work item" (yếu tố công việc), biến chúng thành "work result" (kết quả công việc). Quá trình này diễn ra ngoài chuỗi (off-chain) trong môi trường nội bộ (in-core). **Refine** hoạt động trong môi trường an toàn, có khả năng bị dừng nếu vượt quá giới hạn tài nguyên. Nếu gặp lỗi như **Timeout** hoặc **Panic**, các "work item" sẽ bị đánh dấu là không hợp lệ.
    
    ⇒ Tham khảo thêm: [Refine](https://wiki.polkadot.network/docs/learn-jam-chain#refine-function)
    
- **Accumulate**: Thành phần này nhận đầu ra từ **Refine** (work result) và tích hợp chúng vào trạng thái tổng thể của dịch vụ. **Accumulate** xử lý trên chuỗi (on-chain) và đảm bảo tính hợp lệ cũng như đồng bộ của các kết quả từ nhiều "work item". Nó cũng kiểm soát tài nguyên (weight) để tránh việc tiêu tốn quá nhiều tài nguyên khi tích hợp các báo cáo công việc.
    
    ⇒ Tham khảo thêm: [Accumulate](https://wiki.polkadot.network/docs/learn-jam-chain#accumulate-function) 
    
- **OnTransfer**: Thành phần này xử lý việc chuyển giao thông tin và tài nguyên giữa các dịch vụ. **OnTransfer** chịu trách nhiệm quản lý các giao dịch token giữa các dịch vụ khác nhau, đảm bảo rằng số dư luôn chính xác. Quá trình này cũng được thực thi trên chuỗi (on-chain) để đảm bảo tính bảo mật và minh bạch của các giao dịch.
    
    ⇒ Tham khảo thêm: [OnTransfer](https://wiki.polkadot.network/docs/learn-jam-chain#on-transfer-function)
    
- **Join-Accumulate**: Đây là một giai đoạn đồng bộ, tổng hợp các kết quả từ nhiều lõi (cores) khác nhau trong quá trình **Refine**. **Join-Accumulate** đảm bảo rằng các phần việc không xung đột với nhau và kết quả cuối cùng được kết hợp thành một trạng thái thống nhất, hợp lệ.
- **Authorization (Xác thực quyền hạn)**: Mỗi "Work Package" cần được xác thực bởi một **Authorizer** trước khi được xử lý. **Authorizer** đảm bảo rằng các công việc được ủy quyền và hợp lệ. Nếu một gói công việc không được xác thực, nó sẽ không được xử lý.
![refine-accumulate-376dcd569f7a4b6f1ed20798f522bd0e.png](./image/ServiceJamCore1.png)

---
![refine-accumulate-376dcd569f7a4b6f1ed20798f522bd0e.png](./image/ServiceJamCore2.png)

---
![refine-accumulate-376dcd569f7a4b6f1ed20798f522bd0e.png](./image/ServiceJamCore3.png)

---
![refine-accumulate-376dcd569f7a4b6f1ed20798f522bd0e.png](./image/ServiceJamCore.png)

Tham khảo thêm tại: [Polkadot Forum](https://forum.polkadot.network/t/announcing-polkavm-a-new-risc-v-based-vm-for-smart-contracts-and-possibly-more/3811) 

### **3. PolkaVM**

**Polkadot Virtual Machine (PVM)** là một máy ảo được thiết kế đặc biệt cho mạng lưới Polkadot, đóng vai trò quan trọng trong **Join-Accumulate Machine (JAM)**, một giao thức blockchain được Gavin Wood đề xuất. PVM cho phép thực hiện các smart contract trên Polkadot với hiệu suất và bảo mật cao.

Dựa trên kiến trúc tập lệnh **RISC-V**, PVM tận dụng những lợi thế nổi bật của ISA này, bao gồm:

- **Sandboxing:** PVM có khả năng cô lập quá trình thực thi, đảm bảo tính bảo mật cao cho các smart contract, giúp ngăn chặn các lỗi và tấn công từ bên ngoài.
- **Deterministic Execution:** PVM đảm bảo rằng kết quả của mỗi lần thực thi sẽ giống nhau cho cùng một tập đầu vào, điều này quan trọng trong việc duy trì tính nhất quán và tin cậy trong các giao dịch blockchain.
- **Performance Optimization:** PVM tối ưu hóa hiệu suất với khả năng chuyển đổi linh hoạt giữa các định dạng phần cứng phổ biến như x86, x64 và ARM. Điều này không chỉ cải thiện tốc độ thực thi mà còn giảm thiểu chi phí vận hành nhờ vào việc sử dụng tốt các công cụ như LLVM.

Bản thân PVM thể hiện tính đơn giản, bảo mật và khả năng mở rộng cao. Nó không chỉ có thể được cô lập (sandboxable) mà còn cung cấp nhiều đảm bảo về việc thực thi, tính xác định và thân thiện với việc tính toán chi phí (metering). Khác với các máy ảo khác, PVM được thiết kế để đơn giản và không thiên vị, điều này giúp giảm độ phức tạp trong phát triển và sử dụng.

Việc tích hợp các điểm ngắt được hỗ trợ bởi **RISC-V** dự kiến sẽ thiết lập tiêu chuẩn mới cho mã hóa có khả năng mở rộng trên các nền tảng đa lõi như **JAM**. Đây là một xu hướng cần thiết để mở rộng các thuật toán blockchain và đồng thuận trong tương lai, giúp **PolkaVM** duy trì sự phát triển và thích ứng với những thay đổi công nghệ.

***So sánh với WebAssembly (WASM)***

PolkaVM mang lại hiệu suất vượt trội trong bối cảnh blockchain so với WebAssembly (WASM). Cụ thể, trong khi PolkaVM cung cấp tốc độ biên dịch nhanh gấp 300 lần so với Wasmtime và khả năng thực thi mạnh mẽ, WASM chủ yếu được tối ưu hóa cho các ứng dụng web và không có tính năng sandboxing mạnh mẽ như PolkaVM. Điều này khiến PolkaVM trở thành lựa chọn lý tưởng cho các dự án blockchain cần tốc độ và bảo mật cao hơn.

### **4. Synchronous Communication**

Hàm `onTransfer` trong hệ thống JAM cũng là một hàm thay đổi trạng thái (stateful), cho phép nó sửa đổi trạng thái của các `Services`. Hàm này có khả năng kiểm tra trạng thái của các dịch vụ khác và thực hiện thay đổi đối với trạng thái của chính nó. Chức năng này tạo điều kiện thuận lợi cho việc giao tiếp giữa các dịch vụ, mặc dù theo cách thức bất đồng bộ (asynchronous).

Không giống như nhiều Smart Contract khác, nơi các tương tác diễn ra đồng bộ (synchronously), trong JAM, các thành phần như Smart Contract hoặc dịch vụ tương tác với nhau theo cách bất đồng bộ (asynchronously). Message và Token được gửi đi, và tại một thời điểm sau đó trong cùng một chu kỳ thực thi khoảng 6 giây, phía Services nhận sẽ xử lý chúng.

- Không có phản hồi trực tiếp từ dịch vụ nhận: nếu cần phản hồi, dịch vụ gửi phải khởi tạo một giao dịch mới hoặc thay đổi trạng thái của mình sao cho dịch vụ nhận có thể hiểu và xử lý sau này.
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

### 5. Transactionless

JAM, giới thiệu một khái niệm mới là transactionless. Khác với các block-chain truyền thống hoạt động dựa trên cơ chế chính là transaction. 

Điều này có nghĩa là giao dịch transaction sẽ không diễn ra trực tiếp trong JAM. Thay vào đó, tất cả các hành động đều không cần ký giao dịch (permissionless) và trải qua một giai đoạn Refine.

- Giai đoạn Refine trong giai đoạn này, các service sẽ tinh chỉnh trước dữ liệu đầu vào, biến đổi nó thành các báo cáo công việc bao gồm các kết quả công việc. Sau đó, những kết quả công việc này được chuyển lên chuỗi.

Mặt dù nói là TRANSACTIONLESS thì trong JAM cũng có một vài thông tin cụ thể.**Có 5 loại dữ liệu để lưu :**

- Guarantees
- Assurances
- Judgments
- Preimages
- Tickets

Ba loại đầu tiên tạo thành một phần của khung bảo mật của chuỗi JAM. Guarantees và Assurances bao gồm các validator xác nhận tập thể rằng một kết quả công việc phản ánh chính xác kết quả của mục công việc tương ứng sau khi chuyển đổi qua hàm refine của dịch vụ.

Judgments xảy ra khi tính toàn vẹn của một kết quả công việc được coi là không chắc chắn và một đa số lớn các validator xác nhận tính hợp lệ hoặc không hợp lệ của kết quả đó. Trong trường hợp này, một mục công việc không hợp lệ có thể đã được tích hợp vào trạng thái của dịch vụ và một rollback có thể cần phải xảy ra. Judgments phải xảy ra trong vòng một giờ kể từ khi gửi báo cáo công việc lên chuỗi, trong thời gian đó tính xác thực cuối cùng (finality) tạm thời bị tạm dừng.
Preimages đại diện cho một tính năng được cung cấp bởi chuỗi JAM cho hàm refine. Trong khi hàm refine thường không có trạng thái (stateless), nó có thể thực hiện một hoạt động có trạng thái (stateful): tìm kiếm preimage của một hash. Tính năng này là khía cạnh duy nhất của hàm refine.
Tickets đóng vai trò là các mục nhập ẩn danh vào cơ chế sản xuất khối. Chúng không được yêu cầu ngay lập tức để sản xuất khối; thay vào đó, hệ thống hoạt động hai epoch trước. Cơ chế này là một phần của thuật toán SAFROLE, một phiên bản được tinh chỉnh của thuật toán SASSAFRAS ban đầu.

---

# VI. **Networking**

Jam được thiết kế như một hệ thống phân tán, nơi nhiều node kết nối và giao tiếp với nhau qua một mạng lưới. Mạng lưới này đóng vai trò quan trọng trong việc đảm bảo sự đồng bộ hóa trạng thái và hoạt động hiệu quả của hệ thống.

- QUIC protocol : Mạng lưới của JAM sử dụng [QUIC-Protocol](https://en.wikipedia.org/wiki/QUIC). Điều này cho phép kết nối các node với nhau giữa một số lượng lớn các validator. Thực tế, tất cả hơn 1.000 validator trên Polkadot có thể có kết nối liên tục với nhau mà không gặp vấn đề tiềm ẩn với các socket.
- **Gossip**: Trong JAM Chain, gossip được hạn chế được sử dụng vì nó không không quá cần thiết. JAM không xử lý các giao dịch, do đó không cần phải truyền tải thông tin rộng rãi như trong Polkadot. Thay vào đó, JAM sử dụng giao thức QUIC để kết nối trực tiếp điểm-điểm giữa các validator. Điều này giúp tất cả hơn 1.000 validator trên Polkadot có thể kết nối liên tục với nhau mà không gặp vấn đề với các socket.

---

# **VII. Advantages and Potential of JAM**

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

# **VIII. Challenges and Future Directions**

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

# IX. R**esilience on JAM**

Khả năng phục hồi (Resilience) là một yếu tố quan trọng đối với bất kỳ hệ thống blockchain nào, đặc biệt là trong môi trường phi tập trung của Web3. JAM được thiết kế để đạt được khả năng phục hồi cao thông qua việc kết hợp một số cơ chế bảo mật và khả năng phục hồi độc đáo.

### **1. Bảo mật mạng lưới:**

- **Mã hóa:** JAM sử dụng mã hóa để bảo mật các giao tiếp giữa các node, giúp bảo vệ mạng lưới khỏi các cuộc tấn công mạng lưới như tấn công từ chối dịch vụ (DoS) và tấn công người trong cuộc (MITM).
- **Entropy:** Cơ chế đồng thuận Safrole tạo ra một nhóm entropy có thể được sử dụng bởi các phần khác của giao thức, giúp tăng cường bảo mật và độ ngẫu nhiên cho hệ thống.

### **2. Khả năng phục hồi của chuỗi khối:**

- **Cơ chế đồng thuận:** JAM sử dụng một cơ chế đồng thuận kết hợp giữa Safrole và Grandpa, giúp đảm bảo rằng các khối được thêm vào chuỗi một cách an toàn và không thể bị đảo ngược.
    - **Safrole:** Safrole kiểm soát quá trình sản xuất khối, giúp giảm thiểu khả năng nhiều khối (nhánh) được tạo ra đồng thời. Nó cũng tạo ra một nhóm entropy có thể được sử dụng bởi các phần khác của giao thức.
    - **Grandpa:** Grandpa chịu trách nhiệm cho việc hoàn thiện các khối, đảm bảo rằng một khi một khối được thêm vào blockchain, nó sẽ trở thành một phần vĩnh viễn của lịch sử blockchain.
- **Mã hóa kinh tế:** JAM dựa vào các cơ chế mã hóa kinh tế để khuyến khích các node xác thực hành động trung thực và trừng phạt các hành động bất chính.

### **3. Bảo mật dữ liệu:**

- **Merklization:** JAM sử dụng Merklization để tạo ra một bản sao lưu của dữ liệu trạng thái, giúp bảo vệ dữ liệu khỏi bị mất mát hoặc bị sửa đổi.
- **Kiểm tra tính khả dụng:** Cơ chế kiểm tra tính khả dụng của dữ liệu (Data Availability) đảm bảo rằng dữ liệu được phân phối một cách an toàn và có thể được truy cập bởi tất cả các node.

### **4. Khả năng phục hồi của hệ thống:**

- **Jam được thiết kế để hoạt động hiệu quả ngay cả khi có sự cố xảy ra với một số node trong mạng lưới.** Cơ chế đồng thuận của Jam đảm bảo rằng chuỗi khối vẫn có thể hoạt động ngay cả khi một số node bị lỗi hoặc bị tấn công.
- **Jam có khả năng phục hồi cao (Resilience) bởi vì nó được thiết kế để chống lại các cuộc tấn công và lỗi kỹ thuật.** Các cơ chế bảo mật và khả năng phục hồi của Jam giúp đảm bảo rằng hệ thống có thể hoạt động ổn định và đáng tin cậy trong môi trường phi tập trung.

### **5. Khả năng phục hồi của các dịch vụ:**

- **JAM được thiết kế để đảm bảo rằng các dịch vụ vẫn có thể hoạt động hiệu quả ngay cả khi có sự cố xảy ra với một số node trong mạng lưới.** Cơ chế đồng thuận của Jam đảm bảo rằng chuỗi khối vẫn có thể hoạt động ngay cả khi một số node bị lỗi hoặc bị tấn công.
- **JAM có khả năng phục hồi cao (Resilience) bởi vì nó được thiết kế để chống lại các cuộc tấn công và lỗi kỹ thuật.** Các cơ chế bảo mật và khả năng phục hồi của Jam giúp đảm bảo rằng hệ thống có thể hoạt động ổn định và đáng tin cậy trong môi trường phi tập trung.

### **6. Khả năng phục hồi của các validator:**

- **JAM được thiết kế để đảm bảo rằng các validator vẫn có thể hoạt động hiệu quả ngay cả khi có sự cố xảy ra với một số node trong mạng lưới.** Cơ chế đồng thuận của Jam đảm bảo rằng chuỗi khối vẫn có thể hoạt động ngay cả khi một số node bị lỗi hoặc bị tấn công.
- **JAM có khả năng phục hồi cao (Resilience) bởi vì nó được thiết kế để chống lại các cuộc tấn công và lỗi kỹ thuật.** Các cơ chế bảo mật và khả năng phục hồi của Jam giúp đảm bảo rằng hệ thống có thể hoạt động ổn định và đáng tin cậy trong môi trường phi tập trung.

---

# X. Reference

### Core Documents

- **Graypaper**: [Graypaper.com](https://graypaper.com/)
- **Polkadot Wiki**
    - [Learn JAM Chain](https://wiki.polkadot.network/docs/learn-jam-chain)
    - **GRANDPA Consensus**: [Learn GRANDPA](https://wiki.polkadot.network/docs/learn-consensus#finality-gadget-grandpa)
    - **Sanfrole**: [Learn Sanfrole](https://wiki.polkadot.network/docs/learn-safrole)

### RISC-V Resources

- **What is RISC-V**: [Synopsys Glossary](https://www.synopsys.com/glossary/what-is-risc-v.html)
- **RISC-V Technical Documentation**: [Berkeley - Documents RISC-V](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2016/EECS-2016-118.pdf)

### PolkaVM and Related Technologies

- **RFC-XXXX: "CoreJam"**: [GitHub - CoreJam RFC](https://github.com/polkadot-fellows/RFCs/blob/006a9ff07c3d3bc5316c6bf63b05e966e694cc2d/text/corejam.md)
- **PolkaVM by Koute**: [GitHub Repository](https://github.com/koute/polkavm)
- **PolkaVM Announcement**: [Polkadot Forum - Announcing PolkaVM](https://forum.polkadot.network/t/announcing-polkavm-a-new-risc-v-based-vm-for-smart-contracts-and-possibly-more/3811/5)
- **ParityTech GitHub - PolkaVM**: [GitHub Repository for PolkaVM](https://github.com/paritytech/polkavm)
- **Exploring PolkaVM - RISC-V based VM**: [KusamaXi Article](https://kusamaxi.com/post/polkavm-runs-doom)
- **Hybrid Consensus by OG**:[Hybrid Consensus](https://x.com/openguildwtf/status/1809203505649037391)

### WebAssembly (WASM) and Virtual Machines

- **How WASM Works (Vietnamese)**: [TopDev - WebAssembly](https://topdev.vn/blog/webassembly-tuong-lai-cua-cac-ung-dung-web/)
- **WebAssembly vs. RISC-V**: [Rabbit Hole Blog](https://www.holeoftherabbit.com/2023/11/05/web-assembly-versus-risc-v-but-why/)
- **Stack-based vs. Register-based VMs**: [StackOverflow Discussion](https://stackoverflow.com/questions/164143/registers-vs-stacks)

### Talks and Presentations

- **Gavin Wood on JAM A-Z**: [sub0 Asia 2024 keynote](https://www.youtube.com/watch?v=tdvqkKdFTlw)