---
title: "Attributes in Parent-Child Hierarchies | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "data members [Analysis Services]"
  - "nonleaf members"
  - "MembersWithDataCaption property"
  - "members [Analysis Services]"
  - "members [Analysis Services], data"
  - "leaf members"
  - "parent-child dimensions [Analysis Services]"
  - "MembersWithData property"
ms.assetid: 249971cc-4bcd-44f1-8241-bdacc04d3d38
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Parent-Child Dimension Attributes
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a general assumption is usually made about the content of members in a dimension. Leaf members contain data derived directly from underlying data sources; nonleaf members contain data derived from aggregations performed on child members.  
  
 In a parent-child hierarchy, however, some nonleaf members may also have data derived from underlying data sources, in addition to data aggregated from child members. For these nonleaf members in a parent-child hierarchy, special system-generated child members are created that contain the underlying fact table data. Referred to as *data members*, they contain a value directly associated with a nonleaf member that is independent of the summary value calculated from the descendants of the nonleaf member.  
  
 Data members are available only to dimensions with parent-child hierarchies, and are visible only if allowed by the parent attribute. You can use Dimension Designer to control the visibility of data members. To expose data members, set the **MembersWithData** property for the parent attribute to **NonLeafDataVisible.** To hide data members contained by the parent attribute, set the **MembersWithData** property on the parent attribute to **NonLeafDataHidden**.  
  
 This setting does not override the normal aggregation behavior for nonleaf members; the data member is always included as a child member for the purposes of aggregation. However, a custom rollup formula can be used to override the normal aggregation behavior. The Multidimensional Expressions (MDX) [DataMember](../../mdx/datamember-mdx.md) function gives you the ability to access the value of the associated data member regardless of the value of the **MembersWithData** property.  
  
 The **MembersWithDataCaption** property of the parent attribute provides [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] with the naming template used to generate member names for data members.  
  
## Using Data Members  
 Data members are useful when aggregating measures along organizational dimensions that have parent-child hierarchies. For example, the following diagram shows a dimension that has three levels, representing the gross sales volume of products. The first level shows the gross sales volume for all salespersons. The second level contains the gross sales volume for all sales staff grouped by sales manager, and the third level contains the gross sales volume for all sales staff grouped by salesperson.  
  
 ![Gross sales volume dimension with three levels](../../analysis-services/multidimensional-models/media/agdatamember1.gif "Gross sales volume dimension with three levels")  
  
 Ordinarily, the value of the Sales Manager 1 member would be derived by aggregating the values of the Salesperson 1 and Salesperson 2 members. However, because Sales Manager 1 also can sell products, that member may also contain data derived from the fact table, because there may be gross sales associated with Sales Manager 1.  
  
 Moreover, the individual commissions for each sales staff member can vary. In this case, two different scales are used to compute commissions for the individual gross sales of the sales managers, as opposed to the total of gross sales generated by their salespersons. Therefore, it is important to be able to access the underlying fact table data for nonleaf members. The MDX **DataMember** function can be used to retrieve the individual gross sales volume of the Sales Manager 1 member, and a custom rollup expression can be used to exclude the data member from the aggregated value of the Sales Manager 1 member, providing the gross sales volume of the salespersons associated with that member.  
  
## See Also  
 [Dimension Attribute Properties Reference](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [Parent-Child Dimensions](../../analysis-services/multidimensional-models/parent-child-dimension.md)  
  
  