# PET-SHOP
import javax.swing.*;
import java.awt.event.*;
import java.sql.*;

public class login extends JFrame implements ActionListener
{
    JTextField tu,tp; 
    String un=null,ps=null;
    JLabel lu,lp,lm;
    JButton b; 
    ImageIcon e; 
    Connection c = null;
    Statement stmt;
    ResultSet rs;

    public login()
	{
	setTitle(" LOGIN ");
	e=new ImageIcon("login.jpg");
        tu=new JTextField();  
        tu.setBounds(100,10, 150,20);  
        
	tp=new JTextField();  
        tp.setBounds(100,50, 150,20);  

        lu=new JLabel("UserName");  
        lu.setBounds(10,10, 250,20);      
        lp=new JLabel("Password");  
        lp.setBounds(10,50, 250,20); 
 
	lm=new JLabel("");  
        lm.setBounds(100,80, 250,20);
	
	b=new JButton(e);  
        b.setBounds(50,100,170,70);  
        b.addActionListener(this);    
        
	add(b);add(tu);add(lu);    
        add(tp);add(lp);add(lm);
	setSize(400,400);  
        setLayout(null);  
        setVisible(true);  
	setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	
		try 
                 {
         	    Class.forName("org.sqlite.JDBC");

                    c = DriverManager.getConnection("jdbc:sqlite:shop.db");
                 } 
               catch ( Exception e ) 
                 {
                    System.err.println("Error -> " + e );
                    System.exit(0);
                 }
	}
	 
        public void actionPerformed(ActionEvent e)
	 {  
		
        	un=tu.getText();
		ps=tp.getText();
		if(un.isEmpty()) 
			{
			lm.setText("Enter username");
			 
			}
		else if(ps.isEmpty())
			{
		lm.setText("Enter password");
			}
		else
                 {
		    try
		      {
			String query = "Select * from valid";
       
			stmt = c.createStatement();
	
			rs = stmt.executeQuery(query);
 		
   if(rs.getString("name").equals(un) && rs.getString("pass").equals(ps))
				{
				 
				lm.setText("welcome "+un);
				stmt.close();
				c.close();
				setVisible(false);
				menu ob=new menu();
				}
			       else	
				{
				 
				lm.setText("Wrong Password");
				}
		 	}
			
			catch(Exception E)
			{
			System.out.print("ee"+e);
			}
			
		}
  
          
         }  
	
}
