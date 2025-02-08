when doing reductions, try to keep the same informationm of the problem A, without really altering its instance properties. Meaning, when for example reducing from a graph to a diff data structure. Try to copy all graph properties, in order to convey in some way the same meaning. Copying edges, vertices, (src, dest).



When doing local replacement, We need to think of the common things that is between the 2 problems. Let's say we are reducing from vertex cover to feeback vertex set. We need to think of the things that are common between the 2 problems, edges and cycles. Here A yes is easy to get us to a yes of the other problem. But a No is not trivial. So we should focus on the conditions under which the problem B return False/True, and make the reduction as so. Also here we created cycles for every to adjancent vertices. We can see, than we combine the idea of vertex cover "adjancent vertices" with the notion of the "cycles" for the feeback vertex set. 

When doing the reduction, use all polynomial time properties from problem A.

When writing the correctness proof, we need to always keep in mind, how we get a Yes instance of the target problem, under what conditions... Also, make use of the certificate in problem A, to prove that it has some sense in problem B.


When reducing, use examples, and let's say as an example here, we will take reduction from exact cover 3 to exact cover 4. In this reduction, we need to keep the properties present in problem A, but generate "fake" and "needed" data in problem B, so that we fulfill its conditions. Here we did the creation of arbitrary variables, included in each subsets, in order not to pollute the data in problem A. Here, the reduction is by local replacement method: Al we do is pick some aspect of the known NP-complete problem instance to make up a collection of basic un- its, and we obtain the corresponding instance of the target problem by re- placing each basic unit, in a uniform way, with a different structure
