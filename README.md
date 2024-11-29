# JDBC
How to insert and fetch the data in the ecplise software





package Advancedjava;

import java.sql.*;
import java.util.*;
public class Batchprocessing {

	public static void main(String[] args) 
	{
		Connection c=null;
		
		Scanner sc=new Scanner(System.in);
		
		System.err.println("How many data  you want to insert");
		int count=sc.nextInt();
		
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
	

			c=DriverManager.getConnection("jdbc:mysql://localhost:3306/student_db","root","Root@123");
			 Statement s=c.createStatement();
//			PreparedStatement p=c.prepareStatement("insert into student values(?,?,?)");
//			
//		    
//			
//			for(int i=1;i<=count;i++)
//			{
//				System.out.println("Enter Id:");
//				int id=sc.nextInt();
//				
//				System.out.println("Enter the name:");
//				String name=sc.next();
//				
//				System.out.println("Enter the subject:");
//				String subject=sc.next();
//				
//				
//				    p.setInt(1, id);
//				    p.setString(2, name);
//				    p.setString(3, subject);
//				    p.addBatch();
//				    
//				 
//				}
//			p.executeBatch();
			
			 boolean b=s.execute("select * from student   order by id ");
			 System.out.format("%6s%18s%25s","ID", "NAME","SUBJECT"+"\n");
	        
				System.out.format("-------------------------------------------------------\n");
			
				if(b)
				{
					ResultSet rs=s.getResultSet();
					while(rs.next())
			        {
						System.out.format("%6s%18s%25s",
			            		rs.getInt("id"),
			                    rs.getString("name"),
			            	    rs.getString("subject")+"\n");
						
			        }
				}
			}
			catch(SQLException | ClassNotFoundException e)
		   {
			        e.printStackTrace();
		   }
		// close the connection
		   finally
		  {
			   try 
			   {
				   if(c!=null)
				   {
					   c.close();
				   }
				   
			   }
			   catch(SQLException e)
			   {
				   e.printStackTrace();
			   }
			   
			
		  }
	}
}







/////////////////////output should be  

    ID              NAME                 SUBJECT
-------------------------------------------------------
     1              arun                   tamil
     2              bala                 english
     3             frank                  hindhi
     4             kumar                   maths
     5           gowtham              electronic
     6               don                 history
     7              hari                computer

