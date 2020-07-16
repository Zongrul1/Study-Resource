生成[0,1.0)区间的小数：double d1 = r.nextDouble();  
生成[0,5.0)区间的小数：double d2 = r.nextDouble() * 5;  
生成[1,2.5)区间的小数：double d3 = r.nextDouble() * 1.5 + 1;  
生成-231到231-1之间的整数：int n = r.nextInt();  
生成[0,10)区间的整数：  
int n2 = r.nextInt(10);//方法一  
n2 = Math.abs(r.nextInt() % 10);//方法二  
