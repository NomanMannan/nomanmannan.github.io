---
layout: post
category : Design Patterns
title: Functional Proxy
tagline: "Proxy Pattern"
tags : [proxy, proxy pattern, functional abstraction, delegation]
---
{% include JB/setup %}

Proxy pattern provides pre and post processing before and after delegation to the real object accordingly. 
For example consider a  SimpleCalculator class:


	public class SimpleCalculator implements Calculator<Double, Double, Double> {
		private double result;

		public SimpleCalculator() {
			result = 0.0;
		}

		public Double summation(Double t, Double e) {
			return result = (double) (t + e);// //return the summation of t and e

		}

	}

Suppose in the above example I want to keep log before and after summation calculation. Here I can use proxy pattern for this purpose. Consider the following ProxySimpleCalculator class:


	public class ProxySimpleCalculator implements Calculator<Double, Double, Double> {
			private Calculator calculator; // composition
			private Double result;

		public ProxySimpleCalculator(Calculator calculator) {
			this.calculator = calculator;
			this.result = 0.0;
		}

		public Double summation(Double value1, Double value2) {
			System.out.print("Result Before Summation:: " + result + "\n"); // pre processing
			result = (Double) calculator.summation(value1, value2); // delegation
			System.out.print("Result After Summation:: " + result); // post processing
			return result;
		}

	}

Here for pre and post processing I can use functional abstraction using functor.

Functor Class:


	public class LogFunctor implements Functor<String, String, String> {

		public String pre(String t) {
			System.out.print(t);
			return t;
		}

		public String post(String t) {
			System.out.print(t);
			return t;
		}

	}

ProxySimpleCalculator using Functor:


	public class ProxySimpleCalculator implements Calculator<Double, Double, Double> {
			private Calculator calculator;//composition
			private Functor log;
			private Double result;

		public ProxySimpleCalculator(Calculator calculator, Functor log) {
			this.calculator = calculator;
			this.log = log;
			this.result = 0.0;
		}

		public Double summation(Double value1, Double value2) {
			log.pre("Result Before Summation:: ");//pre processing
			System.out.print(result+"\n");
			result = (Double) calculator.summation(value1, value2);//delegation 
			log.post("Result After Summation:: ");//post processing 
			System.out.print(result);
			return result;
		}

	}  
