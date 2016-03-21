# Guideline for student application 
## General guidelines

* Applications that do not contain at least the minimum information in the template **will not** get a slot.

* The best applications run to several pages (10+) if printed, and show considerable thought and planning.  The application process is longer this year than it has been in some prior years, so this should not be a problem.

* Be sure to follow the general guidelines available in the [GSoC student guide](http://write.flossmanuals.net/gsocstudentguide/writing-a-proposal/).

* If you have questions about details, contact your mentors first.  If you still have choices to make or different possible approaches, explore the most likely ones in your application. The goal of your application is to demonstrate your capability to complete the work of the project over the course of the summer, demonstrate that you've given a fair amount of thought to an implementation approach, and plan, as much as possible, for choices that may change the goals or timeline in the application.

* Once your draft application has been submitted, you may receive comments from other C3G mentors, either listed project mentors or others.  Please respond to the comments promptly and completely.  Being non-responsive before you've even been awarded a slot is not a good sign for the success of your proposal.

* Originality is always welcomed. If you have improvement ideas that go beyong the proposed project scope, by all means include them in your proposal.



## Project Info

Project title: **Flowchart creator for MUGQIC Pipelines**  
Project short title (30 characters): **Flowchart creator**  
URL of project idea page: [idea link](https://bitbucket.org/mugqic/gsoc2016#markdown-header-flowchart-creator-for-mugqic-pipelines)  
## Biographical Information  
Provide a brief (text) biography, and why you think your background qualifies you for this project.  
I am a graduate student pursuing MS in Information System for Big Data and Predictive Analytics Track at [Washington university in St.Louis](http://wustl.edu). I was an undergraduate student at Anhui University of Technology in Information system major. Though I am an information system student, I got a solid programming knowledge structure (programming skills, data structure and algorithm, OS organization) when I was in China.
### Why I think my background qualifies me for this project.  
* I have a solid background of python and OS organization(unix) which help me to be familiar with MUGQICPipeline structure quickly.    
* In addition, in my free time, I have experienced in using Graphviz software and I hava learned the basic knowledge of pipeline flowchart.
* I have experienced in github and bitbucket.

### Why I choose this project
* I am interested in MUGQICPipeline structure. It is the first time for me to know how to control pipeline on clusters with python.
* I am a studious student and my major is data analysis. So I think in the future I can help the community to develop other tools with my major knowledge. 
* I think that pipeline flowchart idea is a cool idea, which makes MUGQICPipeline more user-friendly and concrete.
* I really love this project and the mentor of this project is very kind and patience.

## Contact Information

Student name: Wei Wang

Melange Link_id:  

Student postal address: 304N SKINKER BLVD, APT 3S, ST.LOUIS, MO, U.S.

Telephone(s): +1 314-541-5129 or +86 139-3399-7555

Email(s): wangwei407@wustl.edu or wei0301wang@gmail.com

Other communications channels: Skype/Google+, etc. : 


## Student Affiliation

University: Washington Univisity in St.Louis  

School: School of Engineering & Applied Science

Program: M.S in Information System

Stage of completion: second year

Contact to verify: There is an automatically generated [PDF](http://52.36.214.116/~wangwei407/gsoc2016/Information.pdf) from my university account.


## Schedule Conflicts

This summer, I don't have any other internships or plans, so I can contuibute all my time to this project.

## Mentors

Mentor names: 

Mentor emails: 

Mentor link_ids: 

Have you been in touch with the mentors? When and how? 


## Synopsis (max 150 words)
MUGQIC_PIPELINE program maintains 7 different kinds of pipelines and currently develops 3 others, and each of them contains 10 to 40 steps. My project is an integrated system which will automatically output flowchart based on different steps (e.g 1-20 or 1,4,9,11,20,21-30) and kinds of pipeline (e.g dnaseq,rnaseq) when pipeline is called.

##  Benefits to Community (max 250 words)
Flowchart creator is a user-friendly add-on to MUGQIC_PIPELINE. As metioned in **Synopsis**, MUGQIC_PIPELINE has many different kinds of pipelines and user can decide steps range, in this case, a flowchart contains all information which make MUGQIC_PIPELINE software more user-friendly and concrete. For example, flowchart contains start node (contains pipeline type,time and output path), step node (e.g. step1:convert BAM to FASTQ files), input/output node (e.g. BAM/FAST files) and action node (tell user what action dose the step do). Plus, I will make an integrated Flowchart creator API in pipeline base class so that it will has no requirement that changing the pipeline class in order to add new type pipeline in future. 

## Coding Plan & Methods
Describe perceived obstacles and challenges, and how you plan to overcome them.
###Coding objective:
A Flowchart Creator API which is merged into pipeline base class.
###dependencies
####[Graphviz](http://www.graphviz.org)
Graphviz is open source graph visualization software. Graph visualization is a way of representing structural information as diagrams of abstract graphs and networks. It has important applications in networking, bioinformatics,  software engineering, database and web design, machine learning, and in visual interfaces for other technical domains. 
Graphviz consists of a graph description language named the [DOT language](https://en.wikipedia.org/wiki/DOT_(graph_description_language)) and a set of tools that can generate and/or process.
**Why I choose Graphviz:**
* Graphviz is a mature, stable, open-source and free of charge software. Though it is not a dedicated flowchart or diagramming package, but it's core use case--i.e, efficient and asethetic rendering of objects comprised of nodes and edges, obviously subsumes flowchart drawing
* Graphviz has it's own algorithm to automatically arrange nodes and edge.
* Graphviz provide [many attributes](http://www.graphviz.org/doc/info/attrs.html) to nodes, edges, subgraph. Such as color, size, font, style and url (e.g. When user click on the Trimmoatic node, flowchart will redirect user to trimmomatic [documentation](http://www.usadellab.org/cms/index.php?page=trimmomatic) website)
* Graphviz consists of DOT language which is an easy and concise language to depict a directed graph.
* For example,  
```dot
  digraph G {  
  "MUGQIC PIPELINE START!"->"run step"  
  "run step"->"END"
  }    
  This is an easy directed graph contains 3 nodes, and two edges (-> connects two nodes)
```
####[pydot](http://code.google.com/p/pydot/)
a python interface to graphviz software  
**Why I choose pydot**  
* Pydot is an **open-source** and **light-weighted** python interface to graphviz, the mechanism of pydot is to transfer python code to DOT language and call Graphviz to output the graph.  
For example, use python module pydot to draw the graph    
```python
import pydot  
Graph=pydot.Dot() #create a dot object  
edge1=pydot.Edge('MUGQIC PIPELINE START','run step')  #create a edge between node1 and node2  
edge2=pydot.Edge('run step','END')  
Graph.add_edge(edge1) #add edge1 to Graph  
Graph.add_edge(edge2)  
Graph.write_png('example.png') #output a png graph named 'example'  
```
![example.png](http://52.36.214.116/~wangwei407/gsoc2016/example.png)  

#### Merge Graphviz and python module into MUGQICPipeline (Thanks to mentor Johanna giving me correct direction and clues)
> Add pydot into resources.python_lib.sh and write a bash script Graphviz.sh to install Graphviz software in MUGQICPipeline software

###Flowchart Creator API structure  (challenge) (Thanks to mentor Johanna giving me correct direction and clues)  
I have observed that MUGQIC_PIPELINE software has 7 kinds of pipeline, and the pipeline class structures are as follows:    
![class.png](http://52.36.214.116/~wangwei407/gsoc2016/class.png)  
**In this case, Flowchart Creator API will have 7 kinds of flowchart creator classes and has the same hierarchy as MUGQIC_PIPELINE:**  
```python
1. class MUGQICPipelineCreator  #base class for all creator class
2. class IlluminaRunProcessingCreator(MUGQICPipelineCreator) #(match a pipeline tool)  
3. class BioAssemblyPacoCreator(MUGQICPipelineCreator)  #(match a pipeline tool)    
4. class IlluminaCreator(MUGQICPipelineCreator) #This class is not a pipeline tool, but it is the parent class for DnaSeq, RnaSeq.    
5. class DnaSeqCreator(IlluminaCreator)  #(match a pipeline tool)  
6. class RnaSeqCreator(IlluminaCreator)  #(match a pipeline tool)  
7. class RnaSeqDeNovoAssemblyCreator(IlluminaCreator)  #(match a pipeline tool)  
8. class ChiSeqCreator(DnaSeqGenerator) #(match a pipeline tool)  
9. class DnaSeqHighCoverageCreator #(match a pipeline tool)  
```
> 1. Every Creator class which match a pipeline tool has the same function name related to the step function in pipeline tool. For example, in illumina class, there is a step function "trimmomatic" which clean FASTQ files so that there will be a function named tremmomatic in IlluminaCreator to draw a related action, input/output node for this step.  
2. Every Creator has a class method named draw_flowchart which receive a step name list and call self related functions to draw step nodes and connect them to output.  

### Merge every Creator class into a callable factory class.
#### Register every creator class and its related draw_flowchart function into a dict
```python
from abc import ABCMeta
import six
CREATOR_CLASSES={}
class CreatorRegistry(ABCMeta):
        '''
        metaclass to define creator class
        '''
        registry = CREATOR_CLASSES
        def __new__(mcls,name,bases,memebers):
            cls=super(CreatorRegistry,mcls).__new__(mcls,name,bases,memebers)
            if 'draw_flowchart' in memebers:
                mcls.registry[cls.__name__]=cls.draw_flowchart #store class name and draw_flowchart function in a dict
            return cls
@six.add_metaclass(CreatorRegistry)
class MUGQICPipelineCreator:
        pass
```
> In this case, CREATOR_CLASSES will store all class name(key) and related class method draw_flowchart function(value).

#### Factory class to merge all Creator class callable  
```python
class CreatorFactory:
      def __init__(self):
         self.registry=CREATOR_CLASSES #pass the rigistry CREATOR_CLASSES into CreatorFactory class
      def __call__(clsname,steps):  
          '''
          @param receive a class name and step object list
          '''
          return _check_class(clsname,steps)
      def _check_class(clsname,steps): 
          self.parse_params(steps) 
          Then search self.registry to find out matched clsname and call its related draw_flowchart function to output flowchart
      def parse_params(steps):
          '''
          transfer step object list to a step name (string) list
          '''
          pass  
Creator=CreatorFactory() #create a CreatorFactory object in order to merge Creator API to MUGQICPipeline Software
```
#### Merge Creator API into MUGQICPipeline software
I have observed in core.Pipeline class init() function: 
```python
104.            if self.args.steps:
105.                if re.search("^\d+([,-]\d+)*$", self.args.steps):
106.                    self._step_range = [self.step_list[i - 1] for i in parse_range(self.args.steps)]
107.                else:
108.                    raise Exception("Error: step range \"" + self.args.steps +
109.                        "\" is invalid (should match \d+([,-]\d+)*)!")
110.            else:
111.                self.argparser.error("argument -s/--steps is required!")
```
> ``` self._step_range```is a parsed step object list. In this case, just add ```from CreatorFactory import Creator``` to the header and pass ```self._step_range and class name```to Creator. Like this:

```python
104.            if self.args.steps:
105.                if re.search("^\d+([,-]\d+)*$", self.args.steps):
106.                    self._step_range = [self.step_list[i - 1] for i in parse_range(self.args.steps)]
107.                else:
108.                    raise Exception("Error: step range \"" + self.args.steps +
109.                        "\" is invalid (should match \d+([,-]\d+)*)!")
110.            else:
111.                self.argparser.error("argument -s/--steps is required!")
112.            Creator(self.__class__.__name__, self._step_range) #pass class name and step object list to Creator
```
> In this case, My Creator Factory API has merged into MUGQICPipeline software, and it can output flowchart automatically when pipeline tool is called. 

###Flowchart legend for MUGQIC_PIPELINES  
**input/output node**  
####![input.png](http://52.36.214.116/~wangwei407/gsoc2016/input.png)
**start/end node**  
####![start.png](http://52.36.214.116/~wangwei407/gsoc2016/step.png)
**action node**  
####![action.png](http://52.36.214.116/~wangwei407/gsoc2016/action.png)
###Flowchart expected outcome(selection test)  
####**Selection tests**  
Implement a test flochart in python for 5 first step of the DNAseq pipeline.
the corresponding step are:  
1. picard_sam_to_fastq => generate fastq files from bam files  
2. trimmomatic => clean fastq files  
3. merge_trimmomatic_stats => merge individuals cleaning metrics  
4. bwa_mem_picard_sort_sam => generate bam files from fastq files  
5. picard_merge_sam_files => merge individuals bam files  
#####**My flowchart output**  
##### My flowchart Creator can arrange output in different directions  
1. LR (from left to right)  


![outputLR.png](http://52.36.214.116/~wangwei407/gsoc2016/outputLR.png)


2. TB (from top to bottom)  


![outputTB.png](http://52.36.214.116/~wangwei407/gsoc2016/outputTB.png)


##### My flowchart Creator can output flowchart based on different step range
1. Step (1-4) (To save the space, I use the 'LR' rank for flowchart)  


![outputonefor.png](http://52.36.214.116/~wangwei407/gsoc2016/outputonefor.png)
2. Step (3,4,5)  


![output345.png](http://52.36.214.116/~wangwei407/gsoc2016/output345.png)
## Timeline

(consult GSOC schedule)

Provide a detailed timeline of how you plan to spend your summer, organized by deliverables.  Don't leave testing and documentation for last, as that's almost a guarantee of a failed project. 

What is your contingency plan for things not going to schedule? 
* **23 April** Get to contact mentor and gather information about MUGQICPipeline, such as each pipeline steps details.
* **23 May** Begin coding for project.

###  **Work Period** 
* **23 May-28** Design whole Flowchart Creator API.
* **29 May-3 June** Write documentation for API, including CreatorFactory class and each pipeline Creator class.
* **4 June-6 June** Design and write a test class to make sure that Flowchart Creator create correct start/end node (pipeline name, type, time) and correct sequence of steps. For example, for step list[1,3,4,6,7,19,30] output sequence: 1,3,4,6,7,19,30 is correct, sequence: 1,4,6,3,7,19,30 is wrong.
* **7 June-11 June** Write CreatorFactory class.
* **12 June-18 June** Write Creator classes for each pipeline, which has an order as follows:
![sequence](http://52.36.214.116/~wangwei407/gsoc2016/sequence.png)
* **20 June** Mentors and students can begin submitting mid-term evaluations.
* **27 June** Mid-term evaluations deadline
* **28 June-August 10** Finish the rest part of Creator for pipeline
* **August 10-August 23** Test Flowchart Creator API. Disscuss with MUGQICPipeline team to build the flowchart more concise and beautiful (modify node,edges shape and color and output path and etc.)


## Management of Coding Project

* Clone MUGQICPipeline to [my respository](http://github.com/wangwei407), and make a branch.
* Every week, I will commit the change to the branch. I can test my API on local. And I will report test files to mentor and upload to my branch.
* When I finished the whole API, I will make a pull request to MUGQICPipeline repository.


## Test
#### Test Class description:
* Randomly generate two ouput:  
  1. class name for pipeline type. (e.g. DnaSeq,RnaSeq)    
  2. step object sequence list. For example, step[1,2,3,5,6,7,10,20]  
* Then pass the output to Creator API.
* Get the return of Creator API.
* Check whether or not the class name is matched
* Check whether or not the step output sequence is matched and correct.
* Check whether the step is out of range for pipeline. (e.g. ChiSeq has total 15 steps if Creator receive a step list[1,2,3,4,16] it will raise an out of step range exception)



## Anything Else

