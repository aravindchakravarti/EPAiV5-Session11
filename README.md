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

Class `PolygonIterator` is *ITERATOR* which includes `__iter__` and `__next__` and method. Because *ITERABLE* returned `PolygonIterator`, now `python` will use `__iter__` and `__next__` to fetch the next element.

```python
class PolygonIterator:
    ''' Iterator used by RegConvexPolygon to iterate over different number of edges
    '''
    def __init__(self, obj_reg_conv_poly):
        ''' Bind the iterable to local variable for future accessing
        '''

    def __iter__(self):
        # print("PolygonIterator __iter__ is called")
        return self
    
    def __next__(self):
        ''' if edge is greater than sentinal value then stop iteration
        '''
```

# Fetching the next element 
The `__next__` method is responsible for controlling the iteration over the polygons with different numbers of edges.

### Check the Edge Limit:
The method first checks if the current edge count (self.edge_idx) has exceeded the maximum number of edges allowed (self.obj._max_edges).
If it has, the method raises a `StopIteration` exception, which tells Python that there are no more items to iterate over, effectively stopping the iteration.

### Update the Polygon:
If the current edge count is within the allowed range, the method sets the edges attribute of the `RegConvexPolygon` object (self.obj) to the current edge count (self.edge_idx).
This triggers the recalculation of the polygon's area because the edges setter sets a flag to recalculate the area.

### Calculate and Return Values:
The method then calculates and stores the area and perimeter of the polygon in the variable ret_value.
After that, it increments the edge count (self.edge_idx) by 1, so that the next time __next__ is called, it will process the polygon with one more edge.
Finally, it returns the calculated area and perimeter values.

```python
def __next__(self):
    ''' if edge is greater than sentinal value then stop iteration
    '''
    if self.edge_idx > self.obj._max_edges:
        raise StopIteration
    else:
        ''' Set the edges, which sets calculate_area to True
        '''
        # print("PolygonIterator __next__ is called")
        self.obj.edges = self.edge_idx
        ret_value = self.obj.area, self.obj.perimeter
        self.edge_idx =  self.edge_idx + 1
        return ret_value
```

