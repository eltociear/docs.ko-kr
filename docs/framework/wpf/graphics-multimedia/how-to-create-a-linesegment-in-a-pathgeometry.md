---
title: '방법: PathGeometry에 LineSegment 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- line segments [WPF], creating
- graphics [WPF], line segments
ms.assetid: 0155ed47-a20d-49a7-a306-186d8e07fbc4
ms.openlocfilehash: fc7fbad1e534988a36d85c55c1b6a8249692ad67
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452086"
---
# <a name="how-to-create-a-linesegment-in-a-pathgeometry"></a>방법: PathGeometry에 LineSegment 만들기

이 예제에서는 선분을 만드는 방법을 보여 줍니다. 직선 세그먼트를 만들려면 <xref:System.Windows.Media.PathGeometry>, <xref:System.Windows.Media.PathFigure>및 <xref:System.Windows.Media.LineSegment> 클래스를 사용 합니다.

## <a name="example"></a>예제

다음 예제에서는 (10, 50)에서 (200, 70)로 <xref:System.Windows.Media.LineSegment>를 그립니다. 다음 그림에서는 결과 <xref:System.Windows.Media.LineSegment>를 보여 줍니다. 좌표계를 표시 하기 위해 그리드 배경을 추가 했습니다.

![PathFigure의 LineSegment](./media/graphicsmm-pathgeometrylinesegment.png "graphicsmm_pathgeometrylinesegment") (10, 50)에서 (200, 70)까지 그린 LineSegment

[xaml]

[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]에서는 특성 구문을 사용하여 경로를 설명할 수 있습니다.

```xaml
<Path Stroke="Black" StrokeThickness="1"
  Data="M 10,50 L 200,70" />
```

[xaml]

(이 특성 구문은 실제로 <xref:System.Windows.Media.PathGeometry>의 더 간단한 버전인 <xref:System.Windows.Media.StreamGeometry>를 만듭니다. 자세한 내용은 [경로 태그 구문](path-markup-syntax.md) 페이지를 참조하세요.)

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서는 개체 요소 구문을 사용하여 선분을 그릴 수도 있습니다. 다음 예제는 이전 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 예제와 동일합니다.

```xaml
<Path Stroke="Black" StrokeThickness="1">
  <Path.Data>
    <PathGeometry>
      <PathFigure StartPoint="10,50">
        <LineSegment Point="200,70" />
      </PathFigure>
    </PathGeometry>
  </Path.Data>
</Path>
```

```csharp
PathFigure myPathFigure = new PathFigure();
myPathFigure.StartPoint = new Point(10, 50);

LineSegment myLineSegment = new LineSegment();
myLineSegment.Point = new Point(200, 70);

PathSegmentCollection myPathSegmentCollection = new PathSegmentCollection();
myPathSegmentCollection.Add(myLineSegment);

myPathFigure.Segments = myPathSegmentCollection;

PathFigureCollection myPathFigureCollection = new PathFigureCollection();
myPathFigureCollection.Add(myPathFigure);

PathGeometry myPathGeometry = new PathGeometry();
myPathGeometry.Figures = myPathFigureCollection;

Path myPath = new Path();
myPath.Stroke = Brushes.Black;
myPath.StrokeThickness = 1;
myPath.Data = myPathGeometry;
```

```vb
Dim myPathFigure As New PathFigure()
myPathFigure.StartPoint = New Point(10, 50)

Dim myLineSegment As New LineSegment()
myLineSegment.Point = New Point(200, 70)

Dim myPathSegmentCollection As New PathSegmentCollection()
myPathSegmentCollection.Add(myLineSegment)

myPathFigure.Segments = myPathSegmentCollection

Dim myPathFigureCollection As New PathFigureCollection()
myPathFigureCollection.Add(myPathFigure)

Dim myPathGeometry As New PathGeometry()
myPathGeometry.Figures = myPathFigureCollection

Dim myPath As New Path()
myPath.Stroke = Brushes.Black
myPath.StrokeThickness = 1
myPath.Data = myPathGeometry
```

이 예제는 더 큰 샘플에 속합니다. 전체 샘플을 보려면 [기하 도형 샘플](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/Geometry)을 참조하세요.

## <a name="see-also"></a>참고 항목

- <xref:System.Windows.Media.PathFigure>
- <xref:System.Windows.Media.PathGeometry>
- <xref:System.Windows.Media.GeometryDrawing>
- <xref:System.Windows.Shapes.Path>
- [Geometry 개요](geometry-overview.md)
