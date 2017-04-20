# Getting Started with Model Driven Development and Domain Specific Modeling

## Abstract

As modern systems are becoming more complex so does the need for an approach to increase productivity, reduce rework, and make system integration
and maintainability easier. Model Driven Development (MDD) is introduced as a mean to move the focus of developers from pure coding to analysis and to make system modeling independent of the platform that will be used for system deployment. Using the notion of transformations, MDD can allow a system model to be transformed to the desired programming language on the desired specific platform. This can lead to better portability and interoperability. Domain Specific Languages (DSLs) are fundamental to the concept of MDD. DSLs are modeling languages that target a specific domain and they are typically captured by domain experts.

The aim of this tutorial is to provide an overview about the notion of MDD, review its benefits as well as the challenges that face its adoption. In addition, the tutorial highlights some guidelines to create a domain specific language in practice. Using tools from Eclipse, the tutorial provides a starting point to learn the basics of metamodeling, modeling, and model transformation.


**Keywords**: Model Driven Development (MDD), Model Driven Architecture (MDA), Domain Specific Languages (DSL), Eclipse Modeling Framework (EMF).


## Table of Contents

* [Introduction](#Introduction)
* [Model Driven Architecture (MDA)](#Model_Driven_Architecture)
  * [Types of Models](#Types_of_Models)
  * [MDA Three-Level Architecture](#MDA_Three_Level_Architecture)
* [MDD Benefits](#MDD_Benefits)
  * [Flexible Implementation](#Flexible_Implementation)
  * [Increased Productivity](#Increased_Productivity)
  * [Effective Development, Integration, and Maintenance](#Effective_Development_Integration_and_Maintenance)
* [MDD using Domain Specific Languages (DSLs)](#MDD_using_Domain_Specific_Languages)
  * [What is a Domain Specific Language?](#What_is_a_Domain_Specific_Language)
  * [Advantages of DSL](#Advantages_of_DSL)
  * [Disadvantages of DSL](#Disadvantages_of_DSL)
  * [DSL, UML, and MDD](#DSL_UML_and_MDD)
* [Guidelines to Build a DSL](#Guidelines_to_Build_a_DSL)
  * [Develop and maintain the Metamodel](#Develop_and_maintain_the_Metamodel)
  * [Describe the System Using Multiple Viewpoints](#Describe_the_System_Using_Multiple_Viewpoints)
  * [Validate the Metamodel Keeping the Transformation Simple](#Validate_Metamodel_Keeping_Transformation_Simple)
  * [Create a Useful and Easy-to-Use Code](#Create_Useful_and_Easy_to_Use_Code)
* [MDD Tools Support Using Eclipse](#MDD_Tools_Support_Using_Eclipse)
  * [Eclipse Modeling Framework (EMF)](#Eclipse_Modeling_Framework)
  * [Ecore Metamodel](#Ecore_Metamodel)
  * [Process to Create a Metamodel Using EMF](#Process_to_Create_Metamodel_Using_EMF)
* [Model Transformation](#Model_Transformation)
  * [MOFScript Eclipse Plugin](#MOFScript_Eclipse_Plugin)
  * [Model to Text Transformation Using MOFScript](#Model_to_Text_Transformation_Using_MOFScript)
* [Summary](#Summary)
* [References](#References)



## Introduction
<a name="Introduction"/>

Modern systems are becoming more complex making it increasingly challenging to map requirements to the final product. Managing system complexity and focusing on business needs can be achieved using abstraction and separation of concerns. Modeling is a key approach to do so.

Model-driven Development (MDD) is an approach that represents the software development life-cycle as a modeling and model transformation activities. Models help developers to cope with large and complex systems by allowing them to deal with high level concepts at the right level of abstraction. As a result, the focus of development is moved from writing code for a specific platform to developing an effective solution to satisfy the business needs. Models are used to automate much of the actual coding of applications by generating parts of the Platform Specific Model (PSM) from the Platform Independent Model (PIM) and the actual code from the PSM (to be elaborated later in this tutorial). This way, models are used to drive the code (and not the other way around), keeping the consistency between the model and what the system actually does. MDD gives architects the ability to define and communicate a solution while creating artifacts that become part of the overall solution.

MDD realizes the “Separation of Concerns” principle by separating the business know-how that represents the “WHAT” form of system specifications from the technological know-how that represents the”HOW”. By this, MDD achieves three main objectives; portability, interoperability, and reuse which will eventually lead to an increase in productivity. Domain Specific Languages (DSLs) are very important concept in MDD. DSLs are modeling languages that target a specific domain. It is the responsibility of domain experts to capture domain knowledge into a DSL. Application developers can then use the developed DSL to develop and configure the required system [14].


The very first step to create a DSL is to capture the domain knowledge into a metamodel [16]. Metamodels define the abstract syntax of the DSL [15]. The metamodel should capture the domain definition and scope, domain terminology, and domain concepts and their relationships. A full DSL might be defined using more than one metamodel each describing a certain level of abstraction or a different viewpoint for the given domain. As a result, writing transformations is one of the main activities while defining DSLs. Model transformation is the automatic generation of a target model from a source model, according to a transformation definition. Transformation definition is a set of transformation rules that together describe how a model in the source language (metamodel) can be transformed into a model in the target language (metamodel) [2]. What we need to develop are these transformation rules that take one or more metamodel as an input and generate either text (documentation, code, or configuration scripts) or target models that comply with another output metamodel.


The objective of this tutorial is to provide a starting point to learn the basics of MDD and DSLs. The tutorial covers MDA as a promoted standard for MDD, benefits and drawbacks of MDD, what is a domain specific language and how to define it. To define the language we need to know how to develop metamodels, how to create language editors as well as how to write transformation engines and code/text generators.

The above concepts will be demonstrated using Eclipse-based tools; namely Eclipse Modeling Framework (EMF) for defining metamodels and providing tree-based language editors and MOF Script for writing M2M and M2T  transformations.

The tutorial is organized as follows; section 2 introduces MDA as a promoted standard for MDD. Section 3 discusses the benefits and challenges facing MDD adoption. The definition, advantages, disadvantages, and guidelines to build DSLs are covered in sections 4 and 5. Section 6 and 7 provide hands on experience on tools support for modeling and model transformation using Eclipse tools.


## Model Driven Architecture (MDA)
<a name="Model_Driven_Architecture"/>

Model Driven Architecture (MDA), is a standard promoted by the Open Management Group (OMG). It is an approach to describe IT system specification separating functionality specs from technology platform specs [1]. MDA defines the architecture of models providing guidelines for structuring the specifications that should be represented by these models. One of the main benefits of MDA approach and standards is that it allows the same model to be realized on multiple platforms. This is achieved by defining types of models that represent the system at different levels of abstraction; Business Models and System Models. Transformation between models is a key feature of MDA.

### 2.1 Types of Models
<a name="Types_of_Models"/>

MDA defines two levels of modeling; Business level modeling represented by Computational Independent Models (CIM) and system level modeling represented by Platform Independent Models (PIM) and Platform Specific Models (PSM).

![Alt text](images/MDD/1.png "Figure 1 - Types of Models")

**Computational Independent Model** describes the requirements for a system and the business context in which the system will be used. The model typically describes what a system will be used for, not how it is implemented. CIMs are often expressed in business or domain-specific language and make only limited reference to the use of IT systems when they are part of the business context.


**Platform Independent Model** resolves functional requirements through purely problem-space terms. The model describes how the system will be constructed, without reference to the technologies or platform used to implement the model. Platform Specific Model is a solution model that resolves both functional and non-functional requirements. The model requires information on specific platform related concepts and technologies.

**Model Transformation** is the automatic generation of a target model from a source model, according to a transformation definition which is a set of transformation rules that together describe how a model in the source language can be transformed into a model in the target language. A transformation rule is a description of how one or more constructs in the source language can be transformed into one or more constructs in the target language [2].

### 2.2 MDA Three-Level Architecture

MDA divides the modeling into three layers that are used to finally describe the real world.

![Alt text](images/MDD/2.png "Figure 2 - MDA Three-Layer Architecture")


##TBC!
