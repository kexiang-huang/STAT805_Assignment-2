# Schedule Optimization
## Extension 1: Water Source can only Change flow rate every 4 hours.	

In this extension, the frequency of water source change flow rate is limited. In order to establish a particular formulation to add this constraint for the SAS architecture, we set a function ‘bs’ which represents ‘binary source’ to examine the cycle of source’s activity at least 4 hours. The mathematical formulation subject to the constraint is above. The variable ‘ns’ is not considered in this extension because it would not change and affect the constraint.   

 ![图片 1](https://user-images.githubusercontent.com/55010982/64826655-7bbaae80-d615-11e9-8764-d78b54a3047d.png)	
 
 ![图片 2](https://user-images.githubusercontent.com/55010982/64826706-a147b800-d615-11e9-94cf-0b784abd02e0.png)	
 
 Among them,	
 
 ![3](https://user-images.githubusercontent.com/55010982/64826708-a442a880-d615-11e9-8516-a1b4bca46b69.png)	
 
 ![4](https://user-images.githubusercontent.com/55010982/64826712-a73d9900-d615-11e9-9cfe-91ab47c76062.png)	
 
 ![5](https://user-images.githubusercontent.com/55010982/64826716-a99ff300-d615-11e9-836d-ef5a6f84113d.png)	
 
 The subtraction of two sources’ function is used to ensure the schedule can be divided by numeric 4 integrally when it implements the operation of flow rate transform. The right-hand formula determined the feasibility of flow rate change, the situation when the output value of function ‘bs’ equal zero would be rejected because the difference of two integers which greater than zero on the left hand cannot meet the requirement of inequality. In contrast, both of two reciprocal inequalities are true when ‘bs’ is one. In another word, only once in four hours for the design of sources schedule can change the flow rate, the sources would keep the same or similar flow rate in four hours which originate from the moment of the latest flow rate change till the next cycle. With the establishment of this constraint, the optimal solution still stayed in 1910.25 dollars. However, the distribution of source schedule has been changed refer to Figure. The flow rates produced by Cornwall were normalized at the same rate in four hours per unit.	
 
![6](https://user-images.githubusercontent.com/55010982/64826718-ab69b680-d615-11e9-8b25-052e142ffb2c.png)
![7](https://user-images.githubusercontent.com/55010982/64826719-ad337a00-d615-11e9-8c45-46adcfc7866a.png) 
 Figure 1. The sources schedule without constraint (left) and the sources schedule with constraint (right).	
 
 ## Extension 2: A pump has to run for at least 2 hours.	
 
 ![8](https://user-images.githubusercontent.com/55010982/64826992-bbce6100-d616-11e9-8222-bbc68ba90653.png)	
 
 Among them,	
 
 ![9](https://user-images.githubusercontent.com/55010982/64826996-bf61e800-d616-11e9-8c4f-e5b307053885.png)
 
 ![10](https://user-images.githubusercontent.com/55010982/64826997-c0931500-d616-11e9-9268-9896c5e3e8a2.png)	
 
 ## Extension 3: If a valve is open, it has to stay open at the same flow rate for at least 4 hours.	
 ![11](https://user-images.githubusercontent.com/55010982/64826999-c25cd880-d616-11e9-9bee-7d7cff673f5f.png)
 
 ![12](https://user-images.githubusercontent.com/55010982/64827002-c38e0580-d616-11e9-88a8-4275ef4372d4.png)	
 
 ![13](https://user-images.githubusercontent.com/55010982/64827003-c557c900-d616-11e9-8e7a-15ec461e642a.png)
