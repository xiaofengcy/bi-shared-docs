---
title: "AggregationDesignID Element (ASSL) | Microsoft Docs"
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
---
# AggregationDesignID Element (ASSL)

  Identifies the [AggregationDesign](../objects/aggregationdesign-element-assl.md) element associated with the [Partition](../objects/partition-element-assl.md) element.  
  
## Syntax  
  
```xml  
  
<Partition>  
      ...  
   <AggregationDesignID>...</AggregationDesignID>  
   ...  
</Partition>  
```  
  
## Element Characteristics  
  
|Characteristic|Description|  
|--------------------|-----------------|  
|Data type and length|String|  
|Default value|None|  
|Cardinality|0-1: Optional element that can occur once and only once.|  
  
## Element Relationships  
  
|Relationship|Element|  
|------------------|-------------|  
|Parent elements|[Partition](../objects/partition-element-assl.md)|  
|Child elements|None|  
  
## Remarks  
 The element that corresponds to the parent of **AggregationDesignID** in the Analysis Management Objects (AMO) object model is <xref:Microsoft.AnalysisServices.Partition>. See also <xref:Microsoft.AnalysisServices.AggregationDesign>.  
  
## See Also  
 [AggregationDesign Element &#40;ASSL&#41;](../objects/aggregationdesign-element-assl.md)   
 [Properties &#40;ASSL&#41;](properties-assl.md)  
  
  
