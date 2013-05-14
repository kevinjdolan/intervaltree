Interval Tree Implementation in Java
====================================

## Disclaimer

This project is no longer maintained or supported. If you find this useful and would like to contribute or submit a pull request, I will just make you a contributor.

I wrote this back in 2010, when I was a Sophomore in Undergrad. I have not used it or updated it since then. I was an _okay_ programmer back then, but I've learned a lot since then so no guarantees on quality here. I'm dumping this here because I am taking down my old blog and a lot of people would download this from there.

Released under the [WTFPL](http://en.wikipedia.org/wiki/WTFPL).

## Original release notes from 2010

In a recent Java project, I found myself needing to store several intervals of time which I could access readily and efficiently.  I only needed to build the tree once, so a static data structure would work fine, but queries needed to be as efficient as possible.

I found a data structure that accomplishes just this, and interval tree.

It’s a simple enough data structure, but I couldn’t find any Java implementations for it online.

I then went to coding the data structure at the airport last week, and just finished unit testing it to convince myself everything was good to go.  I’m making it available if you are interested, because it’s really a waste of time to hand-code a well-known data structure.

It uses generic typing for the data object, but requires all the intervals to be expressed in terms of longs.  There are probably some obvious problems with catching programmer error.  For instance, if you search for an interval, but reverse start and end, I don’t know what will happen, nor do I care.

It is a static data structure, meaning it must be rebuilt anytime a change is made to the underlying data.  Rebuilds happen automatically if you try to make a query and it is out-of-sync, but you can build manually by calling .build() if you want to, and you can find out if it is currently in-sync by calling .inSync().

The following code snippet shows you how to use the library:

```
IntervalTree<Integer> it = new IntervalTree<Integer>;();
 
it.addInterval(0L,10L,1);
it.addInterval(20L,30L,2);
it.addInterval(15L,17L,3);
it.addInterval(25L,35L,4);

List result1 = it.get(5L);
List result2 = it.get(10L);
List result3 = it.get(29L);
List result4 = it.get(5L,15L);

System.out.println("Intervals that contain 5L:");
for(int r : result1)
    System.out.println(r);

System.out.println("Intervals that contain 10L:");
for(int r : result2)
    System.out.println(r);

System.out.println("Intervals that contain 29L:");
for(int r : result3)
    System.out.println(r);
     
System.out.println("Intervals that intersect (5L,15L):");
for(int r : result4)
    System.out.println(r);
```

This code would output:

```
Intervals that contain 5L:
1
Intervals that contain 10L:
1
Intervals that contain 29L:
2
4
Intervals that intersect (5L,15L):
3
1
```
