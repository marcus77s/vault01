---
title: "MemoryGraphRAG (Outperforms Every RAG)"
source: "https://www.youtube.com/watch?v=RfAbsdq_b-A"
author:
  - "[[Discover AI]]"
published: 2026-06-03
created: 2026-06-03
description: "Building a Self-Adjudicating Memory Network for RAG.MemGraphRAG: Giving LLMs a Collaborative, Three-Layer Long-Term Memory.All rights w/ authors:MemGraphRAG:..."
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=RfAbsdq_b-A)

## Transcript

**0:00** · Hello community. So great that you are back. Yes, today we talk a further development on rag. You know we had graph rag and now we have a memory graph rag and yeah absolutely we built a new memory graph layer with an ontological layer with three different memory layers and it will improve the performance of our system. And here we have it. This is here from Shia Man University and Gilin University.

**0:26** · Mem graph rag memorybased multi- aent system for the graph retrieval augmented generation. And you sync back to the good old times and said where is my vanilla rack? But forget about it. We have now this new a novel framework that introduces now a memory based multi- aent system to ensure high quality graph construction. And if you're new to this you say hey but why we had graph rag? It was perfect. No, Graphre had three main problems and they now cope with each of their problem.

**1:00** · They found a solution to this problem.

**1:02** · So let's start. Graphre had the problem of automatic irrelevance. Let's call it the noise because the LLM reads here chunks out of the context. It extracts sometimes irrelevant sites and side notes. So for example in a medical text about cancer it might extract to the triplet patient prefers tea over coffee.

**1:23** · This is nice but maybe this is not here really relevant for the amnesis.

**1:29** · Second logical inconsistency or called the lies. Different chunk of text often contradict each other especially have multi sources. Now one says hey Isaac Newton was born in 1643 and the other says no Newton was born in 1645.

**1:44** · And the naive graph rack simply merges now both acts creating a split timeline that confuses now here the downstream retrieval and third problem was the cracks the structural fragmentation without a global taxonomy the graph becomes fragmented and we'll show you how we can cope with this so the same entity might be written here as Newton in one place and Isaac Newton in another

**2:09** · place resulting here in disconnected islands think about this in a threedimensional graph structure that prevent now a multihop retrieval from traversing here the complete database we are logged in here maybe to some graph islands we want to solve this so beautiful and in general you can say if you have here on the x-axis the recall and percentage and on the y-axis the relevance in percentage vanilla racket did great but look where it is positioned no so graph rag achieves a higher recall percentage Absolutely.

**2:41** · So this means it finds more potential clues but it has a catastrophic low relevance because more or less it drowns the LLM in noisy contradictory context. Yes, of course we have hypoor and some GFM rag and everything. And if you are new to my channel, I have a complete uh playlist on YouTube here about rag 3.0 agency. So there's nothing about the vanilla rag.

**3:10** · This is already rag 3.0. So if you want to see here spre or whatever you like, we have a lot a lot of rack systems.

**3:20** · But what is the latest memory graph rag?

**3:23** · This is a three layer global memory that more or less we add here to the graph rag system.

**3:30** · So here you have it compared to the graph rag. Here on the bottom you see me graph rag. So we have the chunking we inject it but we have now three different layers of memory. We build now a hierarchical graph and we will have a good old friend from Google in the retrieval page ranking mechanisms here to extract the facts from all the text passages. So let's start at first we have to have here the memory based indexing of the graph construct itself.

**4:00** · So what we have we have unstructured document where we store thousands and millions of documents. Beautiful. And I will show you later on we have three agents. on the first age and here's the extraction agent. Guess what? And it takes care that it is positioned now in three different memory layers. We have global memory here and the first one is the ontology layer. You know we have here a schema know where we have our graphs either this person rule country or person native location or company create product whatever.

**4:30** · Now for your particular documents this builds now a frequency filter for the stable schema for the top K schemas like I don't know country capital city or person job profession. So the ontology layer stores schemas with the extraction frequency of your training documents. And then we have the factual layer and this is where guess what maintains here the concrete facts. Beautiful.

**4:58** · As I showed you, we have now from two different documents here, Newton birth year birth year 1643 and Newton birth year 1645.

**5:08** · So what's happening from this fact layer? We have now the second agent, our conflict detector agent and understands okay there is a conflict and you know we have to keep the agent simple. Don't give them two jobs, only one job because yeah, LLM is not that capable. And then we hands it over to the next third agent. And the third agent is now a conflict handler. Guess what? This conflict handler looks now at the triplet here of the conflicting triplet looks at the original document and says, "Okay, it can only be one true."

**5:40** · So given here what is the documentation here, it now decides one of them is the correct one. And beautiful. And this is here in the passage layer because here in the passage layer it preserves the original text passages for the evidence grounding. This is here absolutely important.

**6:01** · So you see this is here where we say if we have a debugging here logical debugging what we do we go here to the passage layer and we see exactly here what was the incoming information on why did here the conflict detector and the conflict handler agent choose here a particular document and then if we have all of these memory full of data we build a graph. So we start here in the bottom here with a passage graph. Here we have the entity, the documents, everything is there.

**6:32** · Beautiful. Then we build our fact graph here from the fact memory layer. We have here the entity is for example coach, the relation is job and the entity is I don't know Simpson or John or whatever and the weight is one and then we have the ontology graph in a hierarchical structure here where we have the schema.

**6:54** · So the schema is type is person relation is job the second type is profession and the weight is now five in your unstructured document training data.

**7:04** · So as you see we have now three interconnected graph views. So at first we have the schematic ontology graph derived here from m ontology which encodes here the schema level type relations and the structural constraints of those two.

**7:20** · Then we have here second effect graph constructed here from the memory fact fac fact factual which represents here the un no the instantiated entity relation triple for multihop reasoning and then we have the source evident graphs that grounds you everything in the supported text passages now as I always showed you we have three agent they call it a multi- aent group and for a particular reason I'm going to explain at the end of this video they go with a GPD for omni mini I

**7:49** · don't know if it's available officially from OpenI maybe Omni I think is now here. Yeah, whatever.

**7:57** · And they say okay we need three agent and I showed you already what the agent do. So check mark. Beautiful.

**8:04** · Just to make sure the memory itself is not a passive data store. It is here if you want or it enforces here a two-way relationship. So what we have is a schema instance alignment. So every fact in the fact layer must be governed by a validity rule in the ontology layer. And we have a fact and evidence grounding.

**8:26** · This means every fact in the fact layer is mathematically tethered here to the exact text passage in the passage layer where it was found.

**8:35** · And if a fact is questioned, the system can instantly point to this exact source text. Beautiful.

**8:43** · Now I told you about some disconnected some island in the graphs. No. And to fra to to prevent now this fragmentation here the authors of this paper today of memory graph rack bridges now here with two particular bridging mechanism here.

**8:58** · They bridge the disconnected parts of the graph using here two methods. At first we have a type based bridging simple linking here distinct entities if they share a high level category classification in the ontology layer.

**9:13** · Beautiful. And a similarity based bridging. This is drawing on some invisible or rather weak connection between entities whose hold on to your socks. We are back here to the semantic vector embedding are highly similar ensuring that structural traversal can navigate here across the document boundaries. So we still have here a good old cosine similarity.

**9:37** · This is all done offline and now we come here to the real case real world case online retrieval. So now we come we have an incoming query for me for example.

**9:46** · Yeah. So my question is here now. Great.

**9:50** · So what is happening? As you see we have more or less three steps one two and three. So at first we have memory guarded retrieval and reasoning now in three stages. First multi-layer memory retrieval no which retrieves now candidate schemas facts and passages from the memory because my question is here let's say about physics and I have a lot of physical knowledge here in my memory and in the three different layer beautiful

**10:21** · then second is here the structure aware node initialization what does it mean it simply maps the retrieved evidence to some initial node weights It's based on the semantic relevance and on the structural signals that we have in the network. This is classical. And finally, and this is now the beauty if you want, we have a personalized page rank. Good old Google. Google started out with page rank algorithm when I started here to study. How does Google do its job here?

**10:53** · Page rank hundred of years in the past.

**10:55** · Never mind. We still use this algorithm now here in the online retrieval in the third step. So graph propagation which run here personalized page rank over the heterogeneous graph to rank now globally important notes and passages here for the LLM generation and then all the information is gone here to an agent and this agent now provides the answer here to my question. Great.

**11:21** · So if you want to have it a little bit more in an abstract notation when a user submits a query we have at first a parallel extraction. know the system retrieves the relevant schemas, the relevant facts and the passages from the three global memory layers simultaneously.

**11:36** · So if I have a question about physics, it knows exactly okay somewhere in the memory there's the physics department and just grab all the physics. Then we have the smart reset weights. Now this calculates here the starting weights for the graph nodes. So what it does at first it has to suppress the generic hub categories no like these general terms like person or particle or light or photon no because they don't want to drown out here in the specific notes during this research and then they have to prioritize passages with a high information density.

**12:08** · So documents containing rare highly specific experimental data from my latest experiments. So I know exactly here where my data source is and then yes \[clears throat\] as you know the page rank mechanism it simply runs a propagation walk across the entire graph to let the semantic energy flow outward from the query relevant C nodes and this

**12:33** · means we really identify the most critical paths and passages in this complex graph which are then passed on to the generator LLM to provide an answer to the user. Great. Some might say hey this sounds simple. This is straightforward. There's nothing that we say we have to calculate something mathematically that is crazy. No benchmarks.

**12:53** · So let's have a look. We have here different benchmark hotpot wiki multihop music and on on and then overall. So let's have a look. The artist structured this here in three blocks. The first is a direct zero shot lm inference. So, how good is a llama 38 billion here on a hot pot Q&amp;A? We got a result or a GPD4 Omni Mini. This is it.

**13:21** · And now compare this to the added improvement here because here at the end here, this delta is now here. If I would do this with a GPD4 Omni Mini with this new methodology on this particular benchmark, we would jump here from 38.10 to plus 2826.

**13:40** · in addition. So this would be a significant jump in the performance. If we have just a rag system, a vanilla rack system, you go with the top five.

**13:51** · You see we go from 38.10 to 58.5.

**13:55** · But if you would do it here. Yes. See exactly. And then this is beautiful.

**14:00** · Here you have all the racks is the famous rag system. Yeah. the Microsoft graph rack, the lazy graph rack, the light rag, the hipper rack, the hipper rag 2, the equare graph rack, the GFM rack, the logic rack, the linear rack, and my goodness, I don't know how many other rack systems we have already. And then in the last line, our new memory graph rack system and you see it almost outperforms here every other graph based rag retrieval augmented generation methodology. Beautiful.

**14:30** · And you see here also the added performance jump here in the green boxes. So if we go for a hippo rag. So let's stay here. We have plus 8.27.

**14:46** · Is this percentage or percentage points?

**14:48** · I don't know. Please check in the literature. But you see it is quite a nice and impressive jump.

**14:56** · What else?

**14:59** · I told you there's hardly any new mathematics. So here you have not absolid code for coding here the algorithm and at first here's the memory based indexing the graph construction.

**15:10** · So whatever we went through here, you have it again in a simple soda code structure, but I give you also the GitHub repo, so you don't have to code anything. And of course, the memory guided and the online retrieval and yeah, there's a little bit of filtering going on, but otherwise is exactly like we went through. But you can have this now here. Yeah, with fallback solution to standard drag. Of course, you can implement this. But this is exactly what we went through together.

**15:39** · They are really beautifully detailed.

**15:42** · You see here in the annex then also the prompt used here for let's say the conflict resolution agent. So you have here really the prompt that they used for their experiments. If you want to run them, if you want to modify here their prompt further and you want to see how much you can improve now on their memory graph rag methodology, they provide you all the prompts and everything. And yes, of course, here's the GitHub repo as you see three layer memory structure.

**16:11** · And yeah, this is it. This is the address. And then if you have a look at the memory Python file, he exactly built a three layer memory structure with inter layer connection, schema layer, fact layer, passage layer, and yep, everything is available for you if you want to test it out. Yeah, what I did not mention, yes, it outperforms, but you know there's another benefit that it did not just outperform, but we used so much effort and compute time for the indexation of this complex graph that then when we have the incoming query.

**16:45** · This system is now fast and remember Google page rank this is a real fast system. So here we have the data compare this now and here you have raptor hipper and whatever and at the end here the last column is the retrieval time the classical retrieval time and you see you are with this new methodology faster than any other method that we had up until now.

**17:10** · But of course this is only because we invested quite a lot of time in the preparation in the indexing of the graph in building up this complex graph with the complex memory layers.

**17:22** · No. So do not forget operational if you have it absolutely ultra fast but you have to invest quite a lot of here for your particular training for your particular domain knowledge indexing. Let's say you go with mathematics or theoretical physics or chemistry, biology or medicine or finance, whatever you have.

**17:44** · Yeah. And then I told you and I thought about this why GPD4 omni mini and I thought why is there not the latest claude 4.8 eight or I don't know whatever we have no and it is simple and I noticed just a half sentence but I think the intention was that the authors wanted to show us you don't need the best and the most expensive language model on this planet because even with an old non-topnot LLM these new methods work and all the

**18:17** · data you have seen that I showed you here all the agents were running here at GPT E4 Omni Mini LLM. So you cannot say that this has a high technological complexity or this is here that you have to have to run it in a cloud. No. So if you see it now from this perspective, I have to smile and I say hey this is great that the artist choose such an old non old powerful model. No, that we can run maybe locally.

**18:47** · doesn't have to be a GPD system and the mythology is working and it is stable and is providing you really benefits compared to the other graph rack system.

**18:58** · And this is here something I just wanted to stress out because I get some response. Hey, why is there the latest?

**19:04** · Why is this just a 4.7 and not a 4.8 LLM? Well, sometimes it's good to know this new stuff also runs here on good oldfashioned LLMs that are non-complicated at all and they are non-cloud-based.

**19:19** · I hope you had a little bit of fun, some new insights. Maybe you want to try out this new methodology for your particular domain for your the particular complexity level of your query of your task. Would be great to have some feedback. If you have here some improvement that you really notice that those memory layer provide here an additional benefit for your professional work would be great to see you in my next video.