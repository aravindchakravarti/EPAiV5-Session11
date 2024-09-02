# EPAiV5-Session11
This repo contains assignment solution for EPAiV5 Session 11

# Details
Name: Aravind D. Chakravarti
Email: aravinddcsadguru@gmail.com

# Solution Architecture
In order to make the any object into iterable we need to add `__iter__` method. This will be *ITERABLE*. In the code, we have class `RegConvexPolygon`, which is *ITERABLE*. Whenever we use something like `for` loop, Python will look for this `__iter__` and `RegConvexPolygon` will return its *ITERATOR* `PolygonIterator`

```python
class RegConvexPolygon:
    '''
    Regular Convex Polygon class. A polygon is called "Regular Convex Polygon" if and only if:
        a. Equal Side Lengths: All the sides of the polygon are of equal length.
        b. Equal Angles: All the interior angles are equal.
        c. Convexity: The polygon is convex, meaning all its interior angles are less than 180 degrees, 
           and no part of the polygon "caves in."
   '''
   def __init__(self, edges: int, circum_radius: float, max_edges: int = 10) -> None:
   ...
   # Other code
   ...
   def __iter__(self):
        # print("RegConvexPolygon __iter__ is called")
        return self.PolygonIterator(self)
```


