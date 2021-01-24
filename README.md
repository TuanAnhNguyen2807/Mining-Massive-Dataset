Trình bày Mapreduce và  Spark 
1/ Trình bày Mapreduce
  MapReduce là một khung lập trình cho phép chúng ta thực hiện xử lý phân tán và song song trên các tập dữ liệu lớn trong môi trường phân tán.
  Thuật toán MapReduce chứa hai nhiệm vụ quan trọng, đó là Map và Reduce.
  Map lấy một tập hợp dữ liệu và chuyển đổi thành một tập dữ liệu khác, trong đó các phần tử riêng lẻ được chia nhỏ thành các bộ giá trị (cặp khóa / giá trị). Thứ hai, giảm tác vụ, lấy đầu ra từ bản đồ làm đầu vào và kết hợp các bộ dữ liệu đó thành một bộ nhỏ hơn các bộ giá trị.
  Ưu điểm chính của MapReduce là dễ dàng mở rộng quy mô xử lý dữ liệu qua nhiều nút máy tính. 
  Trong mô hình MapReduce, các nguyên tắc xử lý dữ liệu được gọi là các trình ánh xạ và trình giảm bớt.
  Trình theo dõi công việc gửi mã để chạy trên Trình theo dõi tác vụ
  Bộ theo dõi tác vụ phân bổ CPU và bộ nhớ cho các tác vụ và giám sát các tác vụ trên các nút công nhân
  Các ưu điểm của Mapreduce:
  - Xử Lý song song: MapReduce dựa trên mô hình Divide và Conquer giúp chúng ta xử lý dữ liệu bằng các máy khác nhau. Vì dữ liệu được xử lý bởi nhiều máy thay vì một máy song song, thời gian thực hiện để xử lý dữ liệu sẽ giảm đi rất nhiều
  - Vị trí dữ liệu: MapReduce cho phép chúng ta đưa đơn vị xử lý vào dữ liệu. Vì vậy, dữ liệu được phân phối giữa nhiều nút nơi mỗi nút xử lý một phần dữ liệu nằm trên đó. Điều này cho phép chúng ta có những lợi thế sau:
    + Sẽ rất tiết kiệm chi phí để di chuyển đơn vị xử lý sang dữ liệu.
    + Thời gian xử lý được giảm xuống vì tất cả các nút đang làm việc song song với một phần dữ liệu của chúng.
    + Mỗi nút đều nhận một phần dữ liệu để xử lý và do đó, không có khả năng nút bị quá tải.
 2/ Trình bày Spark
   Spark là một trong những công nghệ mới nhất đang được sử dụng để xử lý Dữ liệu lớn một cách nhanh chóng và dễ dàng.
   Apache Spark là một công cụ xử lý mã nguồn mở mạnh mẽ được xây dựng dựa trên tốc độ, tính dễ sử dụng và phân tích phức tạp, với các API trong Java, Scala, Python, R và SQL.
   Spark là một dự án mã nguồn mở trên Apache.
   Nó được phát hành lần đầu tiên vào tháng 2 năm 2013 và đã bùng nổ phổ biến do dễ sử dụng và tốc độ.
   Nó được tạo ra tại AMPLab ở UC Berkeley.
   Có thể coi Spark như một giải pháp thay thế linh hoạt cho MapReduce
   Spark có thể sử dụng dữ liệu được lưu trữ ở nhiều định dạng khác nhau Cassandra AWS S3 HDFS Và hơn thế nữa.
   MapReduce yêu cầu tệp được lưu trữ trong HDFS, Spark thì không!
   Spark cũng có thể thực hiện các hoạt động nhanh hơn gấp 100 lần so với MapReduce.
   MapReduce ghi hầu hết dữ liệu vào đĩa sau mỗi bản đồ và giảm hoạt động.
   Spark giữ hầu hết dữ liệu trong bộ nhớ sau mỗi lần chuyển đổi.
   Spark có thể tràn sang đĩa nếu bộ nhớ bị lấp đầy.
   Spark RDDS:
      Cốt lõi của Spark là ý tưởng về Tập dữ liệu phân tán có khả năng phục hồi (RDD)
      Tập dữ liệu phân tán phục hồi (RDD) có 4 tính năng chính:
        + Thu thập dữ liệu phân tán
        + Chịu được lỗi
        + Hoạt động song song - từng phần
        + Khả năng sử dụng nhiều nguồn dữ liệu  
   RDD là bất biến, được đánh giá một cách lười biếng và có thể lưu vào bộ nhớ cache
   Có hai loại hoạt động Spark:
      + Sự biến đổi
      + Hành động
 
