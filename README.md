# Apriori-Algorithm
package project1.project1;

import java.io.File;

import org.apache.poi.ss.usermodel.Cell;
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Workbook;
import java.io.File;
import java.util.ArrayList;
import java.util.Iterator;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.xssf.usermodel.XSSFSheet;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;



class Item {
	String ItemSet;
	double Support ;
	float transaction ;
	public Item(String itemSet,int support , float trans)
	{
		ItemSet=itemSet;
		Support=support;
		transaction=trans;
		
	}
	public void PRINT () 
	{
		System.out.print(ItemSet + " " + Support);
	}
}

class Item2
	{	
		int Support ;
		ArrayList<String>Set = new ArrayList<String>();
		public Item2(ArrayList<String> set , int support )
		{	
			for(int i = 0 ; i<set.size() ; i++)
			{
				Set.add(set.get(i));
			}
			Support = support ;	
		}
	}



public class App 
{
	
	//public static ArrayList<Item2> table3 = new ArrayList<Item2>();
	
    public static void main( String[] args ) throws IOException
    {
        int min_support=50;
        double min_conf = 0.33;
        ArrayList<Item2> table3 = new ArrayList<Item2>();
    	File f = new File ("CoffeeShopTransactions.xlsx");
    	ArrayList<Item> Table = new ArrayList<Item>();
    	ArrayList<Item> Association_table = new ArrayList<Item>();
    	ArrayList<Item>Association1_table= new ArrayList<Item>();
    	ArrayList<String> data = new ArrayList<String>();
    	ArrayList<Item2> table2 = new ArrayList<Item2>();
    	
    	
    	Table=load_first_table(f);
    	data=load_data(f);
    	table2=load_second_table(min_support,Table,data);
    	table3=load_third_table(min_support,table2,data);
    	//Association1(min_support,table3,data);
    	
    	//System.out.println(table3.size()+ "sdfsdfsdfsdfsdfsdf");
    	for(int i = 0 ; i<Table.size() ; i++)
		{
			if(Table.get(i).Support<min_support) 
			{
				Table.remove(i);
				i--;
			}
		}
    	
    	
    	/*for(int i = 0 ; i<data.size() ; i++) 
		{
			System.out.println(data.get(i) );
		}*/
    	
    	/*for(int i = 0 ; i<table2.size() ; i++) 
		{
			System.out.println(table2.get(i).ItemSet+  " "   +table2.get(i).Support );
		}*/
    	
    	//System.out.print(table2.size());
    	
    	/*for(int i = 0 ; i<table2.size() ; i++) 
		{
    		for (int j = 0 ; j<2 ; j++) {
    			
    			System.out.print(table2.get(i).Set.get(j) + "  " );
    			//System.out.println();
    			
			//System.out.println(table2.get(i).ItemSet+  " "   +table2.get(i).Support );
    	}
    		System.out.println(table2.get(i).Support);
		}*/
    	//Association_table=Association(min_support,table2,data);
    	
    	for(int i = 0 ; i <Association_table.size() ; i++)
		{
		//System.out.println(Association_table.get(i).ItemSet + " " +Association_table.get(i).Support );
		}
    	
    	/*for(int i = 0 ; i<Table.size() ; i++) 
		{
			System.out.println(Table.get(i).ItemSet+  " "   +Table.get(i).Support );
		}*/
    	/*ArrayList<String> Table = new ArrayList<String>();
        Table.add("ahmedayman");
        Table.add("acb");
        Table.add("bac");
        String word = "ahmed";
        for(int i = 0 ; i<Table.size(); i ++)
        {
            if(Table.get(i).contains(word))
            {
                System.out.println(Table.get(i));
            }
        }*/
    	
    	//System.out.println(table3.size());
    	/*for(int i = 0 ; i<table3.size() ; i++) 
		{
    		for (int j = 0 ; j<table3.get(i).Set.size() ; j++) {
    			
    			System.out.print(table3.get(i).Set.get(j));
    			//System.out.println();
    			
			//System.out.println(table2.get(i).ItemSet+  " "   +table2.get(i).Support );
    	}
    		System.out.println();
    		System.out.println(table3.get(i).Support);
		}*/
    	if(min_support>160) 
    	{
    		Association_table=Association(min_conf,table2,data);
    	}
    	else
    	Association1_table=Association1(min_conf,table3,data);			
    }
	
	public static ArrayList load_data (File f ) throws IOException
	{
		FileInputStream fis = new FileInputStream(f);  
		XSSFWorkbook workbook = new XSSFWorkbook(fis);
		XSSFSheet sheet = workbook.getSheetAt(0);
		Iterator <Row> rowIt =sheet.iterator();
		ArrayList<Item> Table = new ArrayList<Item>();
		ArrayList<String> data = new ArrayList<String>();
		Item hot_chocolate= new Item ("Hot chocolate" , 0,0);Table.add(hot_chocolate);
		Item CaramelBites= new Item ("CaramelBites" , 0,0);Table.add(CaramelBites);
		Item Cookiest= new Item ("Cookies" , 0,0);Table.add(Cookiest);
		Item Coffee= new Item ("Coffee" , 0,0);Table.add(Coffee);
		Item Brownie= new Item ("Brownie" , 0,0);Table.add(Brownie);
		Item Tea= new Item ("Tea" , 0,0);Table.add(Tea);
		Item Cake= new Item ("Cake" , 0,0);Table.add(Cake);
		Item Juice= new Item ("Juice" , 0,0);Table.add(Juice);
		Item Mineral_water= new Item ("Mineral water" , 0,0);Table.add(Mineral_water);
		Item Chocolates= new Item ("Chocolates" , 0,0);Table.add(Chocolates);
		rowIt.next();
		int munimam_support;
		String Old_item="";
		//int a = 0 ;
		while(rowIt.hasNext()) 
		{
			//Item item = new Item ("" , 0) ;
			Row row = rowIt.next();
			Iterator<Cell> cellIterator = row.cellIterator();
			cellIterator.next();
			cellIterator.next();
			cellIterator.next();
			
			while(cellIterator.hasNext()) 
			{
				
				Cell cell = cellIterator.next();
				if(Old_item.equals(cell.toString())) 
				{
					//cellIterator.next();
					data.add(cell.toString());
					//continue;
				}
				else {
				for(int i = 0 ; i<Table.size() ; i++) 
				{	String celll;
					celll = cell.toString();
					//System.out.println(celll + "  " + Table.get(i).ItemSet );
					if(celll.equals(Table.get(i).ItemSet)) {
						Table.get(i).Support++;	
						Old_item=celll;
						data.add(celll);
						
					}
				}
				}
			}
		}
		ArrayList<String> data1 = new ArrayList<String>();
		String item = "" ;
		for(int i = 0 ; i<data.size() ; i++) 
		{
			
			if(i==0) {
				
				item+=data.get(i);
				continue;
				}
				else {
				item+=data.get(i);
				if((i)%3==0) 
				{
					data1.add(item);
					item="";
				}
				}
		}
			
		workbook.close();
		fis.close();
		 
		return data1;
		
	}
	public static ArrayList load_first_table (File f ) throws IOException
	{
	FileInputStream fis = new FileInputStream(f);  
	XSSFWorkbook workbook = new XSSFWorkbook(fis);
	XSSFSheet sheet = workbook.getSheetAt(0);
	Iterator <Row> rowIt =sheet.iterator();
	ArrayList<Item> Table = new ArrayList<Item>();
	ArrayList<String> data = new ArrayList<String>();
	Item hot_chocolate= new Item ("Hot chocolate" , 0,0);Table.add(hot_chocolate);
	Item CaramelBites= new Item ("CaramelBites" , 0,0);Table.add(CaramelBites);
	Item Cookiest= new Item ("Cookies" , 0,0);Table.add(Cookiest);
	Item Coffee= new Item ("Coffee" , 0,0);Table.add(Coffee);
	Item Brownie= new Item ("Brownie" , 0,0);Table.add(Brownie);
	Item Tea= new Item ("Tea" , 0,0);Table.add(Tea);
	Item Cake= new Item ("Cake" , 0,0);Table.add(Cake);
	Item Juice= new Item ("Juice" , 0,0);Table.add(Juice);
	Item Mineral_water= new Item ("Mineral water" , 0,0);Table.add(Mineral_water);
	Item Chocolates= new Item ("Chocolates" , 0,0);Table.add(Chocolates);
	rowIt.next();
	int munimam_support;
	String Old_item="";
	//int a = 0 ;
	while(rowIt.hasNext()) 
	{
		//Item item = new Item ("" , 0) ;
		Row row = rowIt.next();
		Iterator<Cell> cellIterator = row.cellIterator();
		cellIterator.next();
		cellIterator.next();
		cellIterator.next();
		
		while(cellIterator.hasNext()) 
		{
			
			Cell cell = cellIterator.next();
			if(Old_item.equals(cell.toString())) 
			{
				//cellIterator.next();
				continue;
			}
			else {
			for(int i = 0 ; i<Table.size() ; i++) 
			{	String celll;
				celll = cell.toString();
				//System.out.println(celll + "  " + Table.get(i).ItemSet );
				if(celll.equals(Table.get(i).ItemSet)) {
					Table.get(i).Support++;	
					Old_item=celll;
					data.add(celll);
					
				}
			}
			}
			
		}
		
		
	}
		/*for(int i = 0 ; i<Table.size() ; i++) 
		{
			System.out.println(Table.get(i).ItemSet+ " " + Table.get(i).Support );
		}*/
	/*for(int i = 0 ; i<data.size() ; i++) 
	{
		System.out.println(data.get(i));
	}*/
		//System.out.println(Table.size());
		
	workbook.close();
	fis.close();
	 return Table ;  
	}
	public static ArrayList load_second_table (int min_support , ArrayList<Item>Table , ArrayList<String>data ) 
	{	
		ArrayList <Item2> table2 = new ArrayList<Item2>();
		
		
		for(int i = 0 ; i<Table.size()-1 ; i++)
		{
			for(int j = i+1 ; j<Table.size() ; j++)
			{
				ArrayList <String> Set = new ArrayList<String>();
				Item2 item2 = new Item2 (Set,0);
				Item item = new Item( "", 0 , 0 );
				item.ItemSet=Table.get(i).ItemSet;
				Set.add(item.ItemSet);
				item.ItemSet=Table.get(j).ItemSet;
				Set.add(item.ItemSet);
				item2.Set=Set;
				table2.add(item2);		
			}	
		}
		for(int i = 0 ; i<table2.size() ; i++) 
		{
			for(int j = 0 ; j<data.size() ; j++)
			{
				if(data.get(j).contains(table2.get(i).Set.get(0)) && (data.get(j).contains(table2.get(i).Set.get(1))))
						{
							table2.get(i).Support++;
						}
			}
		}
		for(int i = 0 ; i<table2.size() ; i++)
		{
			if(table2.get(i).Support<min_support) 
			{
				table2.remove(i);
				i--;
			}
		}
		
		return table2;
		
	}
	
	public static ArrayList<Item2> load_third_table (int min_support , ArrayList<Item2>table2 , ArrayList<String>data )throws IOException
	{	
		ArrayList<Item2> table3 = new ArrayList<Item2>();
		//System.out.println(table3.size()+"aaaaaaaaaa");
		//boolean x=true,y=true,z=true ;
		//ArrayList <Item2> table3 = new ArrayList<Item2>();
		for(int i = 0 ; i<table2.size()-1 ; i++) 
		{
			ArrayList <String> Set = new ArrayList<String>();
			
			for(int j = i+1 ; j<table2.size() ; j++)
			{
				
				
				//System.out.println("bbbb");
				for(int k = 0 ; k<2 ; k++) 
				{
					
					if(!Set.contains(table2.get(j).Set.get(k))) 
						{
					Set.add(table2.get(j).Set.get(k));
					
			
					if(Set.size()==3) 
					{
						Item2 item2 = new Item2 (Set,0);
						table3.add(item2);
						//System.out.println(Set);
						
						Set.clear();
						
						break;
						//item2 = new Item2 (Set,0);
					}
					//table3.add(item2);	
						}
				}
				
			}
			
			
		}
		//System.out.println(table3.size()+"aaaaaaaaaa");
		/*for(int i = 0 ; i<table3.size() ; i++)
		{
			
			System.out.println(table3.get(i).Set);
		}*/
		
		for(int i = 0 ; i<table3.size() ; i++) 
		{
			int count = 0 ;
			for(int j = i+1 ; j<table3.size() ; j++) 
			{
				for(int k = 0 ; k<3 ; k++) 
				{
					for(int l = 0 ; l<3 ; l++) 
					{
						if(table3.get(i).Set.get(k).equals(table3.get(j).Set.get(l)))
						{
							count++;
							
							if(count>=3) 
							{
								
								table3.remove(j);
								//table3.remove(i-1);
								j--;
								count=0;
								//i--;
								//i--;
								
							}
							break;
						}
						//count=0;
					}
				}
				count=0;
			}	
		}
		//System.out.println(table3.size()+"aaaaaaaaaa");
		
		for(int i = 0 ; i<table3.size() ; i++)
		{
			
			System.out.println(table3.get(i).Set);
		}
		/*System.out.println(table3.size());
		System.out.println(table3.size()+"aaaaaaaaaa");*/
		
		
		for(int i = 0 ; i<table3.size() ; i++) 
		{
			for(int j = 0 ; j<data.size() ; j++)
			{
				if(data.get(j).contains(table3.get(i).Set.get(0)) && (data.get(j).contains(table3.get(i).Set.get(1))) && data.get(j).contains(table3.get(i).Set.get(2)))
						{
							table3.get(i).Support++;
							//break;
						}
			}
		}
		
		
		for(int i = 0 ; i<table3.size() ; i++)
		{
			if(table3.get(i).Support<min_support) 
			{
				table3.remove(i);
				i--;
			}
		}
		//System.out.println(table3.size()+"aaaaaaaaaaaaaaaaaaaa");
		//return table3;
		return table3;
		
		
	}
	

	public static ArrayList<Item> Association (double min_conf , ArrayList<Item2>table2 , ArrayList<String>data )throws IOException
	{
		ArrayList<Item> Association_table = new ArrayList<Item>();
		
		for(int i = 0 ; i <table2.size() ; i++)
		{
			Item item = new Item ("",0,0);
			Item item1 = new Item ("",0,0);
			String Asso = table2.get(i).Set.get(0)+"=>"+table2.get(i).Set.get(1);
			String Asso1 = table2.get(i).Set.get(1)+"=>"+table2.get(i).Set.get(0);
			item.ItemSet=Asso;
			item1.ItemSet=Asso1;
			Association_table.add(item);
			Association_table.add(item1);
			
			for(int j = 0 ; j<data.size() ; j++)
			{
				if(data.get(j).contains(table2.get(i).Set.get(0)))
				{
					item.Support++;				}
				if(data.get(j).contains(table2.get(i).Set.get(1)))
				{
					item1.Support++;
				}
			}

			
			item.Support=table2.get(i).Support/item.Support;
			item1.Support=table2.get(i).Support/item1.Support;
		}
		for(int i = 0 ; i <Association_table.size() ; i++)
		{
			if(Association_table.get(i).Support<min_conf)
			{
				Association_table.remove(i);
				i--;
			}
		}
		
		for(int i = 0 ; i <Association_table.size() ; i++)
		{
		System.out.println(Association_table.get(i).ItemSet + " " +Association_table.get(i).Support );
		}
		return Association_table;
		
	}

	public static ArrayList<Item> Association1 (double min_conf , ArrayList<Item2>table3 , ArrayList<String>data )throws IOException
	{
		ArrayList<Item> Association_table1 = new ArrayList<Item>();
		for(int i = 0 ; i <table3.size() ; i++) 
		{
			Item item = new Item ("",0,0);
			Item item1 = new Item ("",0,0);
			Item item2 = new Item ("",0,0);
			Item item3 = new Item ("",0,0);
			Item item4 = new Item ("",0,0);
			Item item5 = new Item ("",0,0);
			String Asso = table3.get(i).Set.get(0)+"=>"+table3.get(i).Set.get(1)+table3.get(i).Set.get(2);
			String Asso1 =table3.get(i).Set.get(1)+"=>"+table3.get(i).Set.get(0)+table3.get(i).Set.get(2); 
			String Asso2 = table3.get(i).Set.get(2) + "=>" +table3.get(i).Set.get(0)+table3.get(i).Set.get(1) ;
			String Asso3 = table3.get(i).Set.get(0)+table3.get(i).Set.get(1)+"=>"+table3.get(i).Set.get(2);
			String Asso4 = table3.get(i).Set.get(1)+table3.get(i).Set.get(2)+"=>"+table3.get(i).Set.get(0);
			String Asso5 = table3.get(i).Set.get(0)+table3.get(i).Set.get(2)+"=>"+table3.get(i).Set.get(1);
			item.ItemSet=Asso;
			item1.ItemSet=Asso1;
			item2.ItemSet=Asso2;
			item3.ItemSet=Asso3;
			item4.ItemSet=Asso4;
			item5.ItemSet=Asso5;
			//item3.ItemSet=Asso3;
			Association_table1.add(item);
			Association_table1.add(item1);
			Association_table1.add(item2);
			Association_table1.add(item3);
			Association_table1.add(item4);
			Association_table1.add(item5);
			
			for(int j = 0 ; j<data.size() ; j++)
			{
				if(data.get(j).contains(table3.get(i).Set.get(0)))
				{
					item.Support++;				}
				if(data.get(j).contains(table3.get(i).Set.get(1)))
				{
					item1.Support++;
				}
				if(data.get(j).contains(table3.get(i).Set.get(2)))
				{
					item2.Support++;
				}
				if(data.get(j).contains(table3.get(i).Set.get(0)) && data.get(j).contains(table3.get(i).Set.get(1)) )
				{
					item3.Support++; // count 0-1
				}
				if(data.get(j).contains(table3.get(i).Set.get(1)) && data.get(j).contains(table3.get(i).Set.get(2)) )
				{
					item4.Support++; // count 1-2
				}
				if(data.get(j).contains(table3.get(i).Set.get(0)) && data.get(j).contains(table3.get(i).Set.get(2)) )
				{
					item5.Support++; // count 0-2
				}
			}
			item.Support=table3.get(i).Support/item.Support;
			item1.Support=table3.get(i).Support/item1.Support;
			item2.Support=table3.get(i).Support/item2.Support;
			item3.Support=table3.get(i).Support/item3.Support;
			item4.Support=table3.get(i).Support/item4.Support;
			item5.Support=table3.get(i).Support/item5.Support;
			
		}
		for(int i = 0 ; i <Association_table1.size() ; i++)
		{
			if(Association_table1.get(i).Support<min_conf)
			{
				Association_table1.remove(i);
				i--;
			}
		}
		
		for(int i = 0 ; i <Association_table1.size() ; i++)
		{
		System.out.println(Association_table1.get(i).ItemSet + " " +Association_table1.get(i).Support );
		}
		return Association_table1;	
	}
		
    
   
}



