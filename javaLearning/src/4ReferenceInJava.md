 4 different reference in java
 
 http://coding-geek.com/java-the-different-reference-types/
 
 type one: strong reference 
 strong reference is the most common referece in java. 
 sample: Object ob = new Object();
 ob is a strong reference in stack, it points to an instance in heap.
 if memory is not enough, the JVM will throw out "outOfMemoryError" rather than that gc  collects this instance.
 if you don't need this instance, you need to do  ob = null  to declare that, because the strong reference ob is still existing.
 
 if you declare a strong reference in a method:
 public void test(){ Object o = new Object()}  
 when you quit the method, the reference o will quit too, and the instance will be gone.
 
 
 type two: soft reference 
 soft reference is used in some memory-sensitive situation, like in Browser: "back" button; 
 sample: String str = "abc";
         SoftReference<String> sr = new SoftReference<String>(str);
 if memory is not enough, the JVM will do
         str = null; 
         System.gc();
 
 "back" button :
       Browser prev = new Browser();   //get page
       SoftReference sr = new SoftReference(prv); // change to soft reference when you are browsering next page
       if(sr.get() != null)  { rev = (Browse) sr.get()}  //still alive if you want to see the page again
       else { prev = new Browser(); // when memory is not enough, gc will collect it 
       sr = new SoftReference(prev);}  //if you want to see it,  you have to get a new instance
       
type three: weak reference
weak reference has a shorter life-cycle than soft reference. when gc is scanning the area and finds weak reference, gc will collect it.
sample: String str = "ab";
        WeakReference wf = new WeakReference(str);
        str = null;    // diffenrent with soft reference
 if gc finds the weak reference, the JVM will do
         str = null; 
         System.gc();

         
type four: phantom reference
phantom reference is totally diffent with others. it always combines with ReferenceQueue when it is using. it is used to trace the instance
when the instance is ready to be collect by gc.  phandom reference likes a mark.