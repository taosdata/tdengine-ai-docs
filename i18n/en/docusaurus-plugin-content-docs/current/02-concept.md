# Basic Concepts

## Element

In TDasset, an element refers to a physical or logical entity. It can be a specific physical device (such as a car), a subsystem of a physical device (such as the brakes of a car), or even a sensor. It can also be logical, such as a factory, a group, a city, etc.  
Elements are organized and managed in a tree structure, where each node in the tree corresponds to an element. An element can have zero or more child elements, zero or more parent elements, zero or more attributes, zero or more analyses, zero or more panels, zero or more dashboards, and one notification template.

## Child Element / Parent Element

An element can have zero or more child elements. For example, a wind turbine has subsystems such as the rotor system, drive system, power generation system, yaw system, control system, tower and foundation system, and auxiliary system. These systems are all child elements of the wind turbine. Child elements can also have their own child elements, such as the power generation system of a wind turbine having generator and inverter as child elements. A wind farm owns multiple wind turbines, and these turbines are all child elements of the wind farm element.  
Except for the root node, every element has a parent element. For example, the wind farm is the parent element of the wind turbine, and the wind turbine is the parent element of the power generation system. Since elements can also define references, an element can have one or more parent elements. Element references will be introduced in advanced topics.

## Attribute

An element has zero or more attributes. These attributes can be configuration items, static tag values, dynamic time-series data, or result data generated by analyses. In TDasset's design, the actual value of an element's attribute can be stored directly in the TDasset system, or it can be referenced as data and not stored in TDasset.  
A data reference means that an attribute is not stored in TDasset, but is obtained through computation or stored in TDengine or a relational database. Computation means that the attribute is calculated based on the values of other attributes. For example, the power attribute of a smart meter is obtained by multiplying the current and voltage attributes, and you only need to configure the calculation expression. If the attribute value is stored in TDengine or another database, you need to specify the table name and column name.  
For metric-type attributes, you can set limit values, target values, physical units, the number of decimal places to display, and prediction configuration.

## Analysis

An element can have zero or more analyses. Analyses are fully implemented based on TDengine's stream processing. Stream processing can be triggered by sliding windows, event windows, state windows, count windows, session windows, or by a newly written data point. These triggers are based on one or more attributes of the element and must be configured as data references of type TDengine Metric. The actual computation can be an expression, a time window aggregation, or aggregation across multiple elements. The calculation result can be saved to an attribute of the element and can also generate events.

## Event

Every element has associated events, which are generated by the analyses of that element. Events have a start and end time, and also include attribute values or calculation results generated by stream processing that the user wants to record, making event analysis easier. Events can be assigned a severity level and can be set to require acknowledgment.

## Panel / Dashboard

An element can have zero or more dashboards, each containing one or more panels. Panels can also exist independently of dashboards. Each panel visualizes the attributes of an element or its child elements, including trend charts, bar charts, pie charts, tables, statistics, and gauges.

## Notification Rule

For events, notifications can be sent to alert users. The content of the notification can be customized to include any information the user wants. Each element has only one notification template. However, for different event types, you can specify the severity level for sending notifications.

## Element Template

In the real world, there are often multiple devices or entities of the same type, with the same attributes, analyses, dashboards, and panels required. Therefore, TDasset introduces element templates. For elements of the same type, create a template first, and then create specific elements based on the template. This facilitates data standardization and greatly improves configuration efficiency. The element template includes attribute templates, analysis templates, panel templates, dashboard templates, and notification rule templates.