# Capstone
*  LINQ

         1.
         class app {
           static void Main() {
             string[] names = { "Burke", "Connor", "Frank", 
                                "Everett", "Albert", "George", 
                                "Harris", "David" };

             IEnumerable<string> query = from s in names 
                                        where s.Length == 5
                                        orderby s
                                        select s.ToUpper();

             foreach (string item in query)
               Console.WriteLine(item);
           }
         }
         
         
         BURKE
         DAVID
         FRANK
                                    
         2. Lambda Expressions
         Func<string, bool>   filter  = s => s.Length == 5;
         Func<string, string> extract = s => s;
         Func<string, string> project = s => s.ToUpper();

         IEnumerable<string> query = names.Where(filter) 
                                          .OrderBy(extract)
                                          .Select(project);
                                    
                                    
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

*  Standard Query Operators 
    1. Where
    
                  IEnumerable<Product> x = products.Where(p => p.UnitPrice >= 10);
         
       equivalent to 
       
                IEnumerable<Product> x =
                      from p in products
                      where p.UnitPrice >= 10
                      select p;
