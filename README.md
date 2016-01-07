[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.github.mpkorstanje/simmetrics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.github.mpkorstanje/simmetrics-core)
[![Build Status](https://travis-ci.org/mpkorstanje/simmetrics.svg)](https://travis-ci.org/mpkorstanje/simmetrics)
[![Coverage Status](https://coveralls.io/repos/mpkorstanje/simmetrics/badge.svg?branch=develop&service=github)](https://coveralls.io/github/mpkorstanje/simmetrics?branch=develop)

SimMetrics 
==========
A Java library of similarity and distance metrics e.g. Levenshtein distance and Cosine similarity. All similarity metrics return normalized values rather than unbounded similarity scores. Distance metrics return non-negative unbounded scores.

## Usage ##

For a quick and easy use [StringMetrics](./simmetrics-core/src/main/java/org/simmetrics/metrics/StringMetrics.java) contains a collection of well known string metrics.

```java
	String str1 = "This is a sentence. It is made of words";
	String str2 = "This sentence is similar. It has almost the same words";
	
	StringMetric metric = StringMetrics.cosineSimilarity();
	
	float result = metric.compare(str1, str2); //0.4767
```

The [StringMetricBuilder](./simmetrics-core/src/main/java/org/simmetrics/builders/StringMetricBuilder.java) is a convenience tool to build string metrics. Any class implementing StringMetric, ListMetric, SetMetric or MultisetMetric can be used to build a string metric. The builder supports simplification, tokenization, token-filtering, token-transformation, and caching.
For usage see the [examples section](./simmetrics-example/src/main/java/org/simmetrics/example/StringMetricBuilderExample.java).  

For a terse syntax use `import static org.simmetrics.builders.StringMetricBuilder.with;`

```java
	String str1 = "This is a sentence. It is made of words";
	String str2 = "This sentence is similar. It has almost the same words";

	StringMetric metric =
			with(new CosineSimilarity<String>())
			.simplify(Simplifiers.toLowerCase(Locale.ENGLISH))
			.simplify(Simplifiers.replaceNonWord())
			.tokenize(Tokenizers.whitespace())
			.build();

	float result = metric.compare(str1, str2); //0.5720
```

The [StringDistanceBuilder](./simmetrics-core/src/main/java/org/simmetrics/builders/StringDistanceBuilder.java) is a convenience tool to build string metrics. Any class implementing StringMetric, ListMetric, SetMetric or MultisetMetric can be used to build a string metric. The builder supports simplification, tokenization, token-filtering, token-transformation, and caching.
For usage see the [examples section](./simmetrics-example/src/main/java/org/simmetrics/example/StringDistanceBuilderExample.java).  

For a terse syntax use `import static org.simmetrics.builders.StringDistanceBuilder.with;`

```java
	String str1 = "This is a sentence. It is made of words";
	String str2 = "This sentence is similar. It has almost the same words";

	StringDistance metric =
			with(new EuclideanDistance<String>())
			.simplify(Simplifiers.toLowerCase(Locale.ENGLISH))
			.simplify(Simplifiers.replaceNonWord())
			.tokenize(Tokenizers.whitespace())
			.build();

	float result = metric.distance(str1, str2); //3.0000
```