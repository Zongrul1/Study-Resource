
@[TOC]

# **I/O stream:**
```java
import java.io.*;
 
public class fileStreamTest {
    public static void main(String args[]) {
        try {
            byte bWrite[] = { 11, 21, 3, 40, 5 };
            OutputStream os = new FileOutputStream("test.txt");
            for (int x = 0; x < bWrite.length; x++) {
                os.write(bWrite[x]); // writes the bytes
            }
            os.close();
 
            InputStream is = new FileInputStream("test.txt");
            int size = is.available();
 
            for (int i = 0; i < size; i++) {
                System.out.print((char) is.read() + "  ");
            }
            is.close();
        } catch (IOException e) {
            System.out.print("Exception");
        }
    }
}
```
# **PrintWriter & Scanner**
**PrintWriter：**
```java
PrintWriter outputStreamName;
outputStreamName = new PrintWriter(new
FileOutputStream(FileName));
```
**Scanner：**

```java
Scanner StreamObject =
new Scanner(new FileInputStream(FileName));
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190808135614125.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNzc4MTU3OA==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190808135559270.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zNzc4MTU3OA==,size_16,color_FFFFFF,t_70)
# **BufferReader:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190808135743829.png)
# **Object I/O Stream:**

```java
//save the data
    public static void writeObjectToFile(NimPlayer[] p)
    {
        File file =new File("players.dat");
        try{
            file.delete();
        }catch(Exception e){
            e.printStackTrace();
        }
        FileOutputStream out;
        try {
            out = new FileOutputStream(file);
            ObjectOutputStream objOut=new ObjectOutputStream(out);
            int i = 0;
            while(p[i] != null) {
            	objOut.writeObject(p[i]);//write object into the .dat
            	i++;
            }
            objOut.flush();
            objOut.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
    //load the data
    public static void readObjectFromFile(NimPlayer[] p)
    {
        File file =new File("players.dat");
        if(file.exists()) {
	        FileInputStream in;
	        try {
	            in = new FileInputStream(file);
	            ObjectInputStream objIn=new ObjectInputStream(in);
	            int i = 0;
	            while(in.available() > 0) {
	            	p[i]=(NimPlayer) objIn.readObject();//read object from the .dat
	            	i++;
	            }
	            objIn.close();
	        } catch (IOException e) {
	            e.printStackTrace();
	        } catch (ClassNotFoundException e) {
	            e.printStackTrace();
	        }
        }
    }
```
