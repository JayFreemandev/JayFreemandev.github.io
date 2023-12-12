---
layout  : wiki
title   : Why steam is slower than for loop(performance benchmark)
date    : 2022-06-29 19:54:06 +0900
updated : 2022-06-29 19:54:06 +0900
resource: 1E/673069-2E22-4100-9944-E2AF5A4C4572
toc     : true
public  : true
parent  : [[2022]]
latex   : true
---
* TOC
{:toc}

### **Java Stream vs. For Loop: Unveiling the Performance Dynamics**
Java 8 introduced streams, offering code that's often more readable than traditional for loops. Despite the enhanced 
readability, a lingering question persists: Why might Java streams incur a performance hit compared to for loops? 
Let's delve into the intricacies.


### **Quick Conclusion**  
Brian Goetz, a notable figure in the Java community, emphasizes the paramount importance of code clarity and readability. 
For 99% of cases, prioritize clear, maintainable, and correct code.
– [Brian Goetz](https://stackoverflow.com/users/3553087/brian-goetz) -

### **Performance Comparison: Readability as the Deciding Factor**
The general speed differences between streams and loops aren't substantial; their pros and cons are context-dependent. 
Deciding between them should primarily hinge on code readability. Benchmark comparisons, provide insights into the performance 
nuances.

### **Overhead Considerations**  
Functional Interface Overhead:
Functional interfaces use generic parameters, limiting them to reference types. Auto boxing, the conversion of primitives 
to references, introduces overhead. Stream API provides specialized primitive streams (e.g., IntStream) to mitigate this.

External Iterator in For Loop:
For loops use an external iterator, whereas streams rely on internal iteration. Primitive types in for loops often reside 
in the stack, reducing overhead.

When Stream Might Outperform:
Stream performance may excel when dealing with heavy functions and wrapped types, especially when iterator and functional 
costs are significant.

### **JIT compiler is optimized to for loop**  
The Just-In-Time (JIT) compiler tends to optimize for loops more effectively, as illustrated in the provided image.
![Untitled](https://user-images.githubusercontent.com/72185011/206899755-b4286de3-c8b5-44f1-8dec-6c49a17c8496.png)
<br>
<br>

### **Benchmarking Experiment by Adam Ruka**  
Adam Ruka conducted a benchmarking experiment comparing Java 8 Stream API and traditional for loops. Results demonstrated 
comparable performance, with the Stream API occasionally outperforming in specific scenarios.

He was wondering himself and wrote code to benchmark, we can see his original code on [GitHub](https://github.com/skinny85/no-more-loops-benchmark)
There are the result of 10,000 randomly generated Article objects on his computer.

![Untitled 1](https://user-images.githubusercontent.com/72185011/206899762-190c88b7-22c6-4c0e-9b4f-506c878e1025.png)
Adam Ruka’s No More Loops Benchmark result, [https://www.endoflineblog.com/benchmarking-java8-streams](https://www.endoflineblog.com/benchmarking-java8-streams)

Result seem similar loop and stream. first one(getFirstJavaArticle()) by 16%, second one(getDistinctTags()) by 24%. 
The Performance of the Stream API show betters compared to for loop in some cases. Therefore, Performance issue can not 
be a consideration.
<br>  
<br>

### **Other Disadvantages**
- Performance Priority:
Unless your industry demands a 1% performance increase and it's a top priority, 
the marginal performance differences are inconsequential. Choose for loops for general use cases.

- Debuggers:
Debugging stream code might be more challenging than for loops, particularly when stepping through filters and mapping 
operations.

- Cognitive Overhead:
Streams should be avoided for small datasets due to unnecessary memory and CPU overhead.

- Familiarity:
In environments with specific code conventions, the familiarity of for loops might outweigh the benefits of streams.

### **conclusion**
Java streams and for loops should prioritize code readability unless faced with a proven performance bottleneck. 
For most scenarios, the negligible differences in performance do not justify sacrificing code clarity. 
Remember Brian Goetz's advice: "Just write whatever is more readable."

**reference**  
[https://stackoverflow.com/questions/34632008/key-indicators-that-a-java-8-stream-will-run-slower-than-a-for-loop](https://stackoverflow.com/questions/34632008/key-indicators-that-a-java-8-stream-will-run-slower-than-a-for-loop)    
[https://www.endoflineblog.com/benchmarking-java8-streams](https://www.endoflineblog.com/benchmarking-java8-streams)    
[https://stackoverflow.com/questions/44180101/in-java-what-are-the-advantages-of-streams-over-loops](https://stackoverflow.com/questions/44180101/in-java-what-are-the-advantages-of-streams-over-loops)  
[https://devm.io/java/java-performance-tutorial-how-fast-are-the-java-8-streams-118830](https://devm.io/java/java-performance-tutorial-how-fast-are-the-java-8-streams-118830)  