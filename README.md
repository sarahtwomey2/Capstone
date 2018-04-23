# Capstone
*  LINQ

*  LINQ to SQL

         [Table(Name="Customers")]
         public class Customer
         {
            [Column(IsPrimaryKey=true)]
            public string CustomerID;
            [Column]
            public string City;
         }
         
         DataContext: 
         
         // DataContext takes a connection string 
         DataContext db = new   DataContext("c:\\northwind\\northwnd.mdf");
         // Get a typed table to run queries
         Table<Customer> Customers = db.GetTable<Customer>();
         // Query for customers from London
         var q =
            from c in Customers
            where c.City == "London"
            select c;
         foreach (var cust in q)
            Console.WriteLine("id = {0}, City = {1}", cust.CustomerID, cust.City);
