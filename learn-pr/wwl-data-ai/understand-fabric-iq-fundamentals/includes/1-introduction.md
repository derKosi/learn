# Introduction

Imagine you're a data analyst at Lamna Healthcare Medical Center, responsible for helping clinical operations teams understand patient care patterns across your facility. Patient records sit in lakehouse tables while vital signs stream continuously from ICU monitoring equipment into an eventhouse. When hospital administrators ask questions like "Which patients in the ICU have elevated vital signs?" or "How many beds are occupied on the surgical floor?", you need to manually join lakehouse tables with eventhouse streams, translate business terms into technical column names, and write complex queries.

Business users can't explore the data themselves—they depend on you to write queries each time they have a question. By the time you deliver answers, clinical conditions may have already changed.

Microsoft Fabric IQ addresses this by providing a way to define business vocabulary in an ontology, then bind those concepts to your data sources in OneLake. You define concepts such as Patient, Department, and Room with their properties and relationships, creating a semantic layer that both data agents and Graph in Microsoft Fabric can use. 

In this module, you'll discover what Fabric IQ is and how it works. You'll explore the components that work together—ontology items, data agents, Graph in Microsoft Fabric, and Power BI semantic models—and learn when to use each one. You'll also see how ontology modeling shifts your approach from use-case-driven thinking to concept-driven thinking, fundamentally changing how teams collaborate around data.
