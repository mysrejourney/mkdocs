# Introduction to PromQL (Prometheus Query Language)

PromQL is used to get the metrics in Prometheus.
When you run the promql expression, we can get any of the below four types of metric.

1. String (currently unused. `Example: "some string"`)
2. Scalar (floating point numeric value. `Example: 124.28`)
3. Instant vector - It is a set of time-series contains a single sample for each time-series. All sharing the same timestamp.
   
`Example:`

![obs_88.png](../assets/obs_88.png)    

4. Range vector - It is a set of time-series contains a range of data points over time for each time-series.

`Example:`

![obs_89.png](../assets/obs_89.png)    

## Selectors

Selectors are nothing but a filter. It helps to filter the metric for specific parameter.

![obs_90.png](../assets/obs_90.png)   

In the above snapshot, we want to capture the metric for `steal` mode, then we need to use `mode=steal` selector.

![obs_91.png](../assets/obs_91.png)  

## Multiple Selectors

Multiple selectors are nothing but a filter with multiple labels. It helps to filter the metric for specific parameter.

![obs_96.png](../assets/obs_96.png) 


## Range Vector Selectors

Range vector selectors are nothing but a filter over the period of time.

![obs_97.png](../assets/obs_97.png) 

## Matchers

There are four types of matcher.

1. Equality
2. Negative Equality
3. Regular Expression Matcher
4. Negative Regular Expression Matcher

**Equality Matcher**

It checks the label/selector should be equal to the exact value.
In the below case, mode is the selector, and it should exactly match `steal`.
Then the metric can be fetched. 

![obs_91.png](../assets/obs_91.png)  

**Negative Equality Matcher**

It checks the label/selector should not be equal to the exact value.
In the below case, mode is the selector, and except `steal` value, it can bring all other mode metrics.
Then the metric can be fetched. 

![obs_92.png](../assets/obs_92.png)  

**Regular Expression Matcher**

It checks the label/selector should equal to the approximate value with the pattern mentioned in the label.

![obs_93.png](../assets/obs_93.png)  

In the above case, mountpoint has multiple values.
Now if we want to filter all the metrics for the mountpoint starts with `/bo` word.

![obs_94.png](../assets/obs_94.png)  


**Negative Regular Expression Matcher**

It checks the label/selector should not be equal to the approximate value with the pattern mentioned in the label.

![obs_93.png](../assets/obs_93.png)  

In the above case, mountpoint has multiple values.
Now if we do not want to filter all the metrics for the mountpoint starts with `/bo` word.

![obs_95.png](../assets/obs_95.png) 

If we want to filter two values, we can use `|` in the regular expression selector.

![obs_98.png](../assets/obs_98.png) 

## Offset

If you want to check the historic data, you can use offset.

![obs_99.png](../assets/obs_99.png) 

In the above snapshot, the value is displayed that occurred exactly 30 minutes ago from now.


## Modifier

If you want to check the historic data for a specific time, you can use modifier.
For example, I want to see the metric on Thursday, 19 September 2024 06:58:24.
I need to convert the date to epoch time and use it in modifier like below

Thursday, 19 September 2024 06:58:24 = Epoch time is 1726709304

![obs_100.png](../assets/obs_100.png) 

`We can use both offset and modifier in the same promql expression.`

![obs_101.png](../assets/obs_101.png) 


Remember that 

```html
node_cpu_seconds_total{mode="user"} @1726709304 offset 5m = node_cpu_seconds_total{mode="user"} offset 5m @1726709304 
```
`node_cpu_seconds_total{mode="user"}[1m] @1726709304 offset 5m` we can use offset and modifier in range vector as well.

![obs_102.png](../assets/obs_102.png) 

