# ajschmidbauer.github.io
# Use Cases

# Who are Flame Graphs for?

Flame graphs are for you if you're doing something at scale - website, server, program, whatever. If something is done at a large enough scale, the time spent optimizing and finding inefficiencies will pay dividends in the future at scale too. A program would also benefit from flame graph profiling it it simply is very computationally intensive - even if it isn't done in a typical distributed web based scaling fashion.

## How complete should your code be?

Flame graphs are something you use after you've written the code and have it running. Flame Graphs are not very helpful during design, development, and testing.  By using profilers and tools like Flame Graphs you can develop with the philosophy "code now, optimize later". You never truly know what is actually an optimization during development anyways. Another benefit to this philosophy is when optimization is not a priority during development and design, "clever" tricks to "speed-up" the program can stay out of the code (they often do little besides confuse future devs anyways).

## Environment - Large Infrastructure

### How much are companies spending on infrastructure?

Snap, Inc (Snapchat parent company) spends [$1 billion USD](https://www.fool.com/investing/2017/02/09/snap-inc-is-also-spending-1-billion-with-amazon-aw.aspx) annually on AWS infrastructure

Salesforce spends [$400 million USD](http://fortune.com/2016/05/25/salesforce-inks-major-aws-deal/) annually on AWS infrastructure.

Other larger cloud users like Google, Amazon, and Netflix do not publish statistics on this.

Basically, infrastructure, especially cloud infrastructure is not cheap since it effectively eliminates hardware and IT staff costs. Companies spend a lot on infrastructure, and small optimizations can have resounding effects. Because optimizations = faster code = lighter server loads = smaller/fewer server instances.

If a developer, with the right tools, can cause a 1% increase in efficiency, they can potentially save the company $1 million a year. Not only will the developer probably see a nice bonus that year, but a change such as this will have a positive effect on the company's stock prices (which the developer probably has some of) - win win scenario here.

You might be thinking that a 1% efficiency increase across the board sounds far fetched though. And maybe you're right. Let's imagine there is a library (internal or external) used throughout the company on several services. A 10% optimization of this library could easily create a cascading effect across the organization.

In many unoptimized and unprofiled services, there are likely many low hanging optimization fruits giving 10%+ efficiency gains that likely take less than an hour of the developers time to discover and fix.

### So again, why profile and use flame graphs?

After the long winded rant about infrastructure costs and optimization, you should profile and use flame graphs because it's easy and the results (savings) are worthwhile and significant. Something that takes less than an hour can have implications far beyond the cost of time spent.

## Program Types
