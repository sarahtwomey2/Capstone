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
            
    2. Defining relationships
    
             [Table(Name="Customers")]
                  public class Customer
                  {
                     [Column(Id=true)]
                     public string CustomerID;
                     ...
                     private EntitySet<Order> _Orders;
                     [Association(Storage="_Orders", OtherKey="CustomerID")]
                     public EntitySet<Order> Orders {
                        get { return this._Orders; }
                        set { this._Orders.Assign(value); }
                     }
                  }
    3. Querying accross relationships
    
             var q =
                     from c in db.Customers
                     from o in c.Orders
                     where c.City == "London"
                     select new { c, o };
                     
    4. modifying and saving entities
    
             Northwind db = new Northwind("c:\\northwind\\northwnd.mdf");
                  // Query for a specific customer
                  string id = "ALFKI";
                  var cust = db.Customers.Single(c => c.CustomerID == id);
                  // Change the name of the contact
                  cust.ContactName = "New Contact";
                  // Create and add a new Order to Orders collection
                  Order ord = new Order { OrderDate = DateTime.Now };
                  cust.Orders.Add(ord);
                  // Ask the DataContext to save all the changes
                  db.SubmitChanges();

*  Standard Query Operators 
    1. Where
    
                  IEnumerable<Product> x = products.Where(p => p.UnitPrice >= 10);
         
       equivalent to 
       
                IEnumerable<Product> x =
                      from p in products
                      where p.UnitPrice >= 10
                      select p;
