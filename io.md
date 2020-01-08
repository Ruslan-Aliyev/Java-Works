# Java IO

## Many ways of IO in Java

```java
//Check a file's existence. File class. 
//File class create file handles.

import java.io.File;

class MyFile{
	public static void main(String[] args){
		File f = new File ("C:\\Users\\Lief\\Desktop\\Java\\experiment.txt");
		if(f.exists()){System.out.println(f.getName()+" exists");}
	}
}

//-------------------------------------------------------------------------------
//NOTE: Reader+Writers are characters and strings, sometimes badly encoded. Streams are bytes
//-------------------------------------------------------------------------------

//Read file. BufferedReader class. Taking FileReader class.
//Split() method for tokenizing.

import java.io.*;
public class MyBufferReader{
	public static void main(String[] args){
		try {
			BufferedReader br = new BufferedReader(new FileReader(new File("experiment.txt")));	
			String[] tokens;
			for (String x = br.readLine(); x != null ; x = br.readLine()) {
				tokens=x.split("/");
				for(String item:tokens){System.out.print(item);}
			}	
		} 
		catch (IOException e) {}
	}
}

//-------------------------------------------------------------------------------

//Read file. BufferedReader class. Taking InputStreamReader class. (roughly the same codes)

import java.io.*;
public class MyBufferReader{
	public static void main(String[] args){
		try {
			BufferedReader br =new BufferedReader(new InputStreamReader(new FileInputStream("experiment.txt")));
			String[] tokens;
			for (String x = br.readLine(); x != null ; x = br.readLine()) {
				tokens=x.split("/");
				for(String item:tokens){System.out.print(item);}
			}
		} 
		catch (IOException e) {}
	}
}

//-------------------------------------------------------------------------------

//Read file. Scanner class.
//Scanner take input streams, files and strings.
//Scanner can take system.in, File, BufferReader and String.
//Scanner is less efficient that BufferReader and dont benefit from buffer, but is more detailed.

import java.util.Scanner;
import java.io.*;
import java.util.*;
public class MyScanner{
	public static void main(String[] args){
		readFile r = new readFile();
		r.openF();
		r.readF();
		r.closeF();
	}
}
class readFile{
	private Scanner s;
	public void openF(){
		try{s=new Scanner(new File("experiment.txt"));}
		catch(Exception e){}
	}
	public void readF(){
		String line;
		while (s.hasNextLine()){
			line=s.nextLine();
			Scanner t=new Scanner(line);
			t.useDelimiter("/");
			String word;
			while (t.hasNext()){
				word=t.next();
				System.out.print(word+" ");
			}
		}
	}
	public void closeF(){s.close();}
}

//-------------------------------------------------------------------------------

//StringTokenizer can also be used to tokenize input strings.

import java.util.StringTokenizer;
public class MyStringTokenizer {
	public static void main(String[] args) {
 
		String str = "aaa/bbb/ccc";
		StringTokenizer st = new StringTokenizer(str, "/");
 
		while (st.hasMoreElements()) {
			System.out.println(st.nextElement());
		}
	}
}

//-------------------------------------------------------------------------------

//Write to file. Formatter class.
//Formatter create and write to files.

import java.io.*;
import java.lang.*;
import java.util.*;
public class MyWriter{
	public static void main(String[] args){
		createFile g = new createFile();
		g.openFile();
		g.addRecords();
		g.closeFile();
	}
}
class createFile{
	private Formatter f;
	public void openFile(){
		try{f=new Formatter ("..\\experiment.txt");}
		catch(Exception e){}
	}
	public void addRecords(){f.format("%s%s%s","jjj","kkk","lll");}
	public void closeFile(){f.close();}
}

//-------------------------------------------------------------------------------

//Write to file. FileWriter class.
//Can be inefficient if there are many small writes

FileWriter file = new FileWriter("foo.txt");
file.write("foobar");
file.close();

//-------------------------------------------------------------------------------

//Write to file. BufferedWriter class.
//Efficient when there are many small writes, cos writes are buffered then wrote.

BufferedWriter bf = new BufferedWriter(new FileWriter("foo.txt"));
bf.write("foobar");
bf.close();

//-------------------------------------------------------------------------------

//Write to file. FileOutputStream inside OutputStreamWriter class.
//OutputStreamWriter converts bytes to writer

OutputStreamWriter os = new OutputStreamWriter(new FileOutputStream(new File("experiment.txt")));
os.write("hello");
os.close();

//-------------------------------------------------------------------------------
```

### Rename

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Java-Works/master/Illustrations/renameFile.PNG)

### Delete

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Java-Works/master/Illustrations/deleteFile.PNG)

### Append

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Java-Works/master/Illustrations/appendTextFile.PNG)
											
### Read .csv file

```java		
import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
 
public class ReadCsv {
  public static void main(String[] args) {
	ReadCsv obj = new ReadCsv();
	obj.run();
  }
 public void run() {
	BufferedReader br = null;
	String line = "";
	try {
		br = new BufferedReader(new FileReader("test.csv"));
		while ((line = br.readLine()) != null) {
			String[] tokens = line.split(",");
			System.out.println(""+tokens[0] + " , " + tokens[1]);
			br.close();
		}
	}
	catch (Exception e) {} 
  }
}
```
					
### Write .csv file

```java
import java.io.FileWriter;
import java.io.IOException;
 
public class GenerateCsv
{
   public static void main(String [] args)
   {
	   generateCsvFile("test.csv"); 
   }
 
   private static void generateCsvFile(String sFileName)
   {
	try
	{
	    FileWriter writer = new FileWriter(sFileName);
 
	    writer.append("DisplayName");
	    writer.append(',');
	    writer.append("Age");
	    writer.append('\n');
 
	    writer.append("MY NAME");
	    writer.append(',');
	    writer.append("26");
        writer.append('\n');
 
	    writer.append("YOUR NAME");
	    writer.append(',');
	    writer.append("29");
	    writer.append('\n');
 
	    //generate whatever data you want
 
	    writer.flush();
	    writer.close();
	}
	catch(IOException e){} 
    }
}
```
