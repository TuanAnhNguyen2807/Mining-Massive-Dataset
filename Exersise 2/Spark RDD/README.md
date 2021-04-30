<h1><i>Spark RDD </i></h1>
<h3><b>1. Giới thiệu </b></h3>
<p><b>RDD (Resilient Distributed Dataset)</b> còn được gọi là tập dữ liệu phân tán khả năng phục hồi. Đây là cấu trúc dữ liệu cơ bản của Apache Spark, là một tập hợp bất biến của các đối tượng tính toán trên các nút khác nhau của cụm.</p>
<p><b>Giải mã tên RDD:</b></p>
<li><b>Có khả năng phục hồi</b>, tức là có khả năng chịu lỗi với sự trợ giúp của đồ thị dòng RDD (DAG) và do đó có thể tính toán lại các phân vùng bị thiếu hoặc hỏng do lỗi nút.</li>
<li><b>Phân tán</b>, vì dữ liệu nằm trên nhiều nút.</li>
<li><b>Tập dữ liệu</b> đại diện cho các bản ghi dữ liệu mà bạn làm việc. Người dùng có thể tải tập dữ liệu ra bên ngoài, có thể là tệp JSON, tệp CSV, tệp văn bản hoặc cơ sở dữ liệu thông qua JDBC không có cấu trúc dữ liệu cụ thể. </li>
<p>Do đó, mỗi và mọi tập dữ liệu trong RDD được phân vùng một cách hợp lý trên nhiều máy chủ để chúng có thể được tính toán trên các nút khác nhau của cụm. RDD có khả năng chịu lỗi tức là Nó có khả năng tự phục hồi trong trường hợp bị lỗi.</p>
<p><b>Có 3 cách để tạo RDD trong Spark:</b><br>
1. Sử dụng parallelized collection.<br>
2. Từ tập dữ liệu bên ngoài (Tham chiếu tập dữ liệu trong hệ thống lưu trữ bên ngoài).<br>
3. Từ apache spark RDD hiện có.</p>
<p>Spark RDD cũng có thể được lưu vào bộ nhớ đệm và phân vùng theo cách thủ công. Bộ nhớ đệm có lợi khi chúng ta sử dụng RDD nhiều lần. Và phân vùng thủ công là rất quan trọng để cân bằng chính xác các phân vùng. Nói chung, các phân vùng nhỏ hơn cho phép phân phối dữ liệu RDD một cách bình đẳng hơn, giữa nhiều người thực thi hơn. Do đó, ít phân vùng hơn giúp công việc trở nên dễ dàng.</p>
<h3><b>2. Tại sao cần RDD trong Spark </b></h3>
<p><b>Các định nghĩa đằng sau khái niệm RDD là:</b></p>
<li>Các thuật toán lặp lại.</li>
<li>Các công cụ khai thác dữ liệu tương tác.</li>
<li>DSM (Bộ nhớ dùng chung phân tán) là một khái niệm trừu tượng rất chung chung, nhưng tính tổng quát này khiến việc triển khai một cách hiệu quả và có khả năng chịu lỗi khó hơn trên các cụm</li>
<li>Trong hệ thống máy tính phân tán, dữ liệu được lưu trữ trong kho lưu trữ phân tán ổn định trung gian như HDFS hoặc Amazon S3. Điều này làm cho việc tính toán công việc chậm hơn vì nó liên quan đến nhiều hoạt động IO, sao chép và tuần tự hóa trong quy trình.</li>
<p>Thách thức chính trong việc thiết kế RDD là xác định một giao diện chương trình cung cấp khả năng chịu lỗi một cách hiệu quả. Để đạt được khả năng chịu lỗi một cách hiệu quả, các RDD cung cấp một dạng bộ nhớ dùng chung bị hạn chế, dựa trên sự chuyển đổi chi tiết hơn là các bản cập nhật chi tiết cho trạng thái chia sẻ.<br>
Spark tiết lộ RDD thông qua API tích hợp ngôn ngữ. Trong API tích hợp, mỗi tập dữ liệu được biểu diễn dưới dạng một đối tượng và quá trình chuyển đổi có liên quan đến việc sử dụng phương thức của các đối tượng này.</p>
<h3><b>3. Tính năng của Spark RDD </b></h3>
<p><b>Một số tính năng của Apache Spark RDD là:</b></p>
<img src="https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/sites/2/2017/08/features-of-RDD-in-spark.jpg">
<ol type = "i">
<b><li>In-memory Computation (Tính toán trong bộ nhớ)</li></b>
<p>Spark  RDD có cung cấp khả năng tính toán trong bộ nhớ . Nó lưu trữ các kết quả trung gian trong bộ nhớ phân tán (RAM) thay vì lưu trữ ổn định (đĩa).</p>
<b><li>Lazy Evaluations (Đánh giá lười biếng) </li></b>
<p>Tất cả các phép biến đổi trong Apache Spark đều lười biếng, ở chỗ chúng không tính toán kết quả của chúng ngay lập tức. Thay vào đó, họ chỉ nhớ các phép biến đổi được áp dụng cho một số tập dữ liệu cơ sở.<br>
Spark tính toán các phép biến đổi khi một hành động yêu cầu kết quả cho chương trình điều khiển. Làm theo hướng dẫn này để tìm hiểu sâu về Đánh giá Lười biếng của Spark. </p>
<b><li> Fault Tolerance (Khả năng chịu lỗi)</li></b>
<p>Spark RDD có khả năng chịu lỗi vì chúng theo dõi thông tin dòng dữ liệu để tự động xây dựng lại dữ liệu bị mất khi bị lỗi. Họ xây dựng lại dữ liệu bị mất khi thất bại bằng cách sử dụng dòng, mỗi RDD nhớ cách nó được tạo từ các bộ dữ liệu khác (bằng các phép biến đổi như bản đồ, tham gia hoặc nhómBy) để tạo lại chính nó. Làm theo hướng dẫn này để nghiên cứu sâu hơn về khả năng chịu lỗi RDD .</p>
<b><li>Immutability (Tính bất biến)</li></b>
<p>Dữ liệu được chia sẻ an toàn trên các quy trình. Nó cũng có thể được tạo hoặc truy xuất bất cứ lúc nào giúp dễ dàng lưu vào bộ nhớ đệm, chia sẻ và nhân rộng. Vì vậy, nó là một cách để đạt được tính nhất quán trong tính toán.</p>
<b><li>Partitioning (phân vùng)</li></b>
<p>Phân vùng là đơn vị cơ bản của tính song song trong Spark RDD. Mỗi phân vùng là một phân chia dữ liệu hợp lý có thể thay đổi được. Người ta có thể tạo một phân vùng thông qua một số biến đổi trên các phân vùng hiện có.</p>
<b><li>Persistence (Sự bền bỉ)</li></b>
<p>Người dùng có thể nêu những RDD nào họ sẽ sử dụng lại và chọn chiến lược lưu trữ cho chúng (ví dụ: lưu trữ trong bộ nhớ hoặc trên Đĩa).</p>
<b><li>Coarse-grained Operations (Hoạt động chi tiết thô)</li></b>
<p>Nó áp dụng cho tất cả các phần tử trong bộ dữ liệu thông qua bản đồ hoặc bộ lọc hoặc nhóm theo hoạt động.</p>
<b><li>Location-Stickiness (Vị trí - Độ dính)</li></b>
<p>RDD có khả năng xác định ưu tiên vị trí để tính toán các phân vùng. Tùy chọn vị trí đề cập đến thông tin về vị trí của RDD. Các  DAGScheduler  đặt phân vùng theo cách như vậy mà nhiệm vụ gần dữ liệu càng nhiều càng tốt.</p>
</ol>
<h3><b>4. Hoạt động của Spark RDD </b></h3>
<p>RDD trong Apache Spark hỗ trợ hai loại hoạt động:</p>
<li>Transformation</li>
<li>Actions</li>
<ol type="i">
<b><li>Transformation</li></b>
<p>Spark RDD Transformations là các  hàm  sử dụng một RDD làm đầu vào và tạo ra một hoặc nhiều RDD làm đầu ra. Chúng không thay đổi RDD đầu vào (vì RDD là bất biến và do đó người ta không thể thay đổi nó), nhưng luôn tạo ra một hoặc nhiều RDD mới bằng cách áp dụng các phép tính mà chúng đại diện, ví dụ như Map (), filter (), ReduceByKey (), v.v.</p>
<p>Một số phép biến đổi nhất định có thể được pipelined, đây là một phương pháp tối ưu hóa mà Spark sử dụng để cải thiện hiệu suất của các phép tính. Có hai loại phép biến hình: phép biến hình hẹp, phép biến hình rộng.</p>
<p><b>a. Biến hình hẹp</b></p>
<p>Nó là kết quả của ánh xạ, bộ lọc và sao cho dữ liệu chỉ từ một phân vùng duy nhất, tức là nó tự cung cấp. Một RDD đầu ra có các phân vùng với các bản ghi bắt nguồn từ một phân vùng duy nhất trong RDD mẹ. Chỉ một tập hợp con giới hạn của các phân vùng được sử dụng để tính toán kết quả.<br>
Spark nhóm các phép biến hình thu hẹp dưới dạng một giai đoạn được gọi là  pipelining.</p>
<img src="https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/sites/2/2017/08/spark-narrow-transformation-1.jpg">
<p><b>b. Biến hình rộng</b></p>
<p>Nó là kết quả của các hàm giống như groupByKey () và ReduceByKey (). Dữ liệu cần thiết để tính toán các bản ghi trong một phân vùng duy nhất có thể nằm trong nhiều phân vùng của RDD mẹ. Các phép biến đổi rộng còn được gọi là  phép biến hình trộn  vì chúng có thể có hoặc không phụ thuộc vào một lần trộn.</p>
<img src="https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/sites/2/2017/08/spark-wide-transformation.jpg">
<b><li>Actions</li></b>
<p>Actions là các hoạt động RDD tạo ra các giá trị không phải RDD. Chúng hiện thực hóa một giá trị trong chương trình Spark. Một hành động là một trong những cách để gửi kết quả từ người thực thi đến trình điều khiển. First(), take(), reduce(), collect(), the count() là một số Hành động trong spark.<br>
Khi Hành động xảy ra, nó không tạo ra RDD mới, không giống như transformation. Do đó, các hành động là các hoạt động RDD không cung cấp giá trị RDD. Hành động lưu trữ giá trị của nó đối với trình điều khiển hoặc hệ thống lưu trữ bên ngoài. Nó đưa sự lười biếng của RDD vào chuyển động.</p>
</ol>
<h3><b>5. Giới hạn của Spark RDD </b></h3>
<img src="https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/sites/2/2017/08/limitations-of-rdd-1.jpg">
<ol>
<b><li>No inbuilt optimization engine (Không có công cụ tối ưu hóa sẵn có)</li></b>
<p>Khi làm việc với dữ liệu có cấu trúc, RDD không thể tận dụng lợi thế của các trình tối ưu hóa nâng cao của Spark bao gồm trình tối ưu hóa chất xúc tác và công cụ thực thi Tungsten . Các nhà phát triển cần tối ưu hóa từng RDD dựa trên các thuộc tính của nó.</p>
<b><li>Handling structured data (Xử lý dữ liệu có cấu trúc)</li></b>
<p>Không giống như Dataframe và bộ dữ liệu, RDD không suy ra lược đồ của dữ liệu đã nhập và yêu cầu người dùng chỉ định nó.</p>
<b><li>Performance limitation (Giới hạn hiệu suất)</li></b>
<p>Là các đối tượng JVM trong bộ nhớ, RDD liên quan đến chi phí của Bộ sưu tập rác và Tuần tự hóa Java, những thứ này rất tốn kém khi dữ liệu phát triển.</p>
<b><li>Storage limitation (Giới hạn lưu trữ)</li></b>
<p>RDDs suy giảm khi không có đủ bộ nhớ để lưu trữ chúng. Người ta cũng có thể lưu trữ phân vùng RDD đó trên đĩa không vừa với RAM. Do đó, nó sẽ cung cấp hiệu suất tương tự như các hệ thống song song dữ liệu hiện tại.</p>
</ol>
<h3><b>6. Kết luận - Spark RDD </b></h3>
<p>Kết luận với RDD, những thiếu sót của Hadoop MapReduce là rất cao. Do đó, nó đã được Spark RDD khắc phục bằng cách đưa vào xử lý trong bộ nhớ, tính bất biến, v.v. Nhưng có một số hạn chế của RDD. Ví dụ: Không có tối ưu hóa sẵn có, giới hạn lưu trữ và hiệu suất, v.v.</p>

<h3><b>tài liệu tham khảo </b></h3>
[Link 1](https://en.wikipedia.org/wiki/RDD) <br>
[Link 2](https://laptrinh.vn/books/apache-spark/page/apache-spark-rdd) <br>
[Link 3](https://intellipaat.com/blog/tutorial/spark-tutorial/programming-with-rdds/)


