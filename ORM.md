Giới thiệu:
ORM là gì ? Chắc trong giới công nghệ thông tin, hẳn ai cung nghe đến nó và cũng hiểu định nghĩa, khái niệm về nó. Nhưng để các bạn nắm rõ hơn ORM, bài viết dưới đây sẽ giới thiệu đến các bạn khái niệm, lợi ích của nó.
Chi tiết:
ORM là một phương pháp lập trình để chuyển đổi từ mô hình database sang mô hình đối tượng.
ORM có nhiều thuận lợi hơn so với những phương pháp truy cập dữ liệu (data access) khác:
· ORM tự động hóa việc chuyển đổi từ object sang table và từ table sang object, giúp giảm thời gian và chi phí phát triển
· ORM cần ít code hơn store procedures, thay thế số lượng lớn store procedudres cần phát triển
· Tăng tốc độ thực thi của hệ thống
Một giải pháp ORM tốt sẽ giúp ứng dụng nhanh hơn và dễ hỗ trợ hơn.

Impedance Mismatch là một trong những lý do quan trọng nhất để sử dụng những công cụ ORM

Ví dụ một mô hình dữ liệu có 2 table: Customers và Accounts. Thông thường, chúng ta sẽ tạo mô hình object với 2 class tương ứng với 2 table này:

Nhưng mô hình object trên thiếu tính linh động và khả năng mở rộng, do đó chúng ta nên thiết kế lại để thêm inheritance và abstraction, làm mô hình gần hơn với thực tế:


Chúng ta có thể thấy rõ ràng sự không đối xứng (mismatch) giữa mô hình dữ liệu và mô hình object trong trường hợp này. Trong database, hoàn toàn chấp nhận được khi chứa toàn bộ thông tin của Person và PersonName trong một table Customers. Nhưng để tăng tốc độ thực thi, việc bảo trì và sự linh hoạt; một object lớn nên được chia thành nhiều object nhỏ.
* * LINQ (Language Integrated Query)
LINQ là một framework mở rộng mới trong .NET 3.5. Trước đây, chúng ta phải viết thêm T-SQL hoặc dùng một công cụ của hãng thứ ba để viết truy vấn trong .NET code, với LINQ người dùng có thể viết những truy vấn để truy cập dữ liệu một cách tự nhiên bằng những ngôn ngữ .NET. LINQ cũng được hỗ trợ kiểm tra cú pháp, IntelliSense…

LINQ cung cấp một cú pháp thống nhất để lấy dữ liệu từ bất cứ object nào có thi hành interface IEnumerable<T>: arrays, collections, dữ liệu từ database, XML…
var query = from e in employees
where e.id == 1
select e.name;

Dùng những từ khóa C#, chúng ta có thể viết code truy cập dữ liệu như một phần của
C# và trình biên dịch C# sẽ có thể kiểm tra type safety và thậm chí logical consistency.
LINQ cung cấp một số lượng hàm rất phong phú để thực hiện những truy vấn phức tạp,
hỗ trợ kết hợp dữ liệu, joins, sắp xếp...

Linq to Sql (LTS)
LTS là công cụ ORM đầu tiên của Microsoft, đây là một framework đi kèm với những công cụ giúp cho quá trình phát triển dễ dàng hơn. Nó cho phép chúng ta tạo mô hình và truy vấn một database trong .NET code. LTS cũng hỗ trợ xử lý transaction, view, store procedure…
So sánh phương pháp truy vấn kiểu cũ dùng DataSet, Adapter, store procedure… với LTS:

Lấy dữ liệu:
	SqlConnection con = new SqlConnection(connectionString);
	DataSet ds = new DataSet(); SqlDataAdapter adapter = new SqlDataAdapter
	("Select * from Customers", con);
	adapter.Fill(ds);
	return ds;

Lấy dữ liệu dùng LTS:
	DataContext db = new DataContext(connectionString);
	Table<Customer> tab = db.GetTable<Customer>();
	return tab;

Thêm dữ liệu:
	using (SqlConnection conn = BaseDao.GetConnection())
	{
	SqlCommand cmd = new SqlCommand("spCustomers_Insert", conn);
	cmd.CommandType = CommandType.StoredProcedure;
	cmd.Parameters.AddWithValue("@id", customer.CustomerID);
	cmd.Parameters.AddWithValue("@name", customer.CustomerName);
	…
	cmd.ExecuteNonQuery();
	}

Thêm dữ liệu dùng LTS:
	DataContext db = new DataContext(connectionString);
	Table<Customer> tab = db.GetTable<Customer>();
	tab.InsertOnSubmit(customer);
	db.SubmitChanges();

LTS ngắn gọn, tự nhiên hơn, truy vấn dữ liệu trực tiếp dùng cú pháp của những ngôn ngữ .NET hướng đối tượng thay vì phải tạo một số lượng lớn store procedure để thực hiện các chức năng thêm, xóa, cập nhật…

