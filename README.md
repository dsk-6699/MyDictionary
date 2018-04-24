# MyDictionary
A simple command line java program which can be used to search for meanings of the stored words in a properties file,if the word is not present we can add it to the file,at the same time we can delete unnecessary/learnt words.


/* A simple Dictionary database that uses a property list. */ 
import java.io.*; 
//import java.net.URL;
import   java.util.*; 
import java.lang.*;
import   java.util.Scanner;
class MyDictionary {  
public static void main(String args[])throws IOException
{
Properties ht = new Properties(); 
//URL url=ClassLoader.getSystemResource("ht.properties");
//ht.load(url.openStream());
BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
String word, meaning,d; 
StringBuffer mean=new StringBuffer("");
int count=0;
//Scanner meaning=new Scanner(System.in);
int n,m;
FileInputStream fin = null; 
boolean changed = false; 
// Try to open MyDictionary.dat file. 
try { 
fin = new FileInputStream("MyDictionary.dat"); 
} 
catch(FileNotFoundException e) 
{  
// ignore missing file 
}
 /* If file already exists, load existing things */ 
 try { 
 if(fin != null) { 
 ht.load(fin); fin.close(); } } 
 catch(IOException e) 
 { System.out.println("Error reading file."); } 
//PropertiesConfiguraton ht=new PropertiesConfiguration(MyDictionary.properties);
System.out.println("Welcome to MyDictionary");
do{
System.out.println("1.Update 2.Meaning 3.Display All 4.No.of Entries 5.Delete 6.Exit");
n=Integer.parseInt(br.readLine());
switch(n)
{
case 1:// Let user enter new words and meanings. 
 //Scannner meaning=new Scanner(System.in());
 do { 
 System.out.println("Enter new WORD" + " ('quit' to stop): "); 
 word = br.readLine(); if(word.equals("quit")) 
 continue; 
 System.out.println("Enter Meaning: "); 
do
 {mean.append(System.getProperty("line.separator"));
 mean.append(br.readLine());
 
 count++;
 } while(!mean.substring(mean.length()-1).equals("/"));
 meaning=mean.toString(); 
// ht.setProperty(word,meaning);
// ht.save();
ht.put(word, meaning); 
 changed = true; } while(!word.equals("quit")); 
 // If  data has changed, save it. 
 if(changed) 
 { 
 FileOutputStream fout = new FileOutputStream("MyDictionary.dat"); 
 ht.store(fout, "My Dictionary"); fout.close(); }
 //Hashmap<String,String> hm=new HashMap<String,List<String>>((Map) ht);
//List<String> values=new ArrayList<String>();
break;
case 2: // Look up numbers given a name. 
 do { 
 System.out.println("Enter Word for the meaning" + " ('quit' to quit): "); 
 word = br.readLine(); if(word.equals("quit")) 
 continue; 
 meaning = (String) ht.get(word); 
 System.out.println("Meaning : ");
 System.out.println(meaning);
 } while(!word.equals("quit"));
break;
case 3:
List<String> keys=new ArrayList<String>();
for(String key:ht.stringPropertyNames())
keys.add(key);
Collections.sort(keys);
Iterator<String> itr=keys.iterator();
while(itr.hasNext())
System.out.println(itr.next()+" ");
break;
case 4:
System.out.println("Number of ENTRIES= "+ht.size());
break;
case 5:do{System.out.println("Enter Word to be deleted(quit to exit)");
d=br.readLine();
ht.remove(d);
System.out.println("deleted");
changed=true;}while(!d.equals("quit"));
if(changed) 
 { 
 FileOutputStream fout = new FileOutputStream("MyDictionary.dat"); 
 ht.store(fout, "My Dictionary"); fout.close(); }
break;
case 6:System.exit(0);
default:System.out.println("Wrong Option");
}
//System.out.println("PRESS ANY NUMBER TO RETURN TO MENU EXCEPT 0");
//m=Integer.parseInt(br.readLine());
}while(true);
}}
/*
Drawbacks
1.case sensitive
2.can't check if word is there or no
3.deletion is not perfect
*/
