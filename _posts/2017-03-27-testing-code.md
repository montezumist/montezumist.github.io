---
title: "Testing the display of code with different type of highlighting"
excerpt: This post shows code highlighting
tags: [highlighting, rouge]
---

In this post I am going to write some code, and then at some point, I will update the _sass/_syntax.css to update the highlight schema that is used here.

The following code snipped is highlighted using Rouge:
```python
def topological_sort(self):
    """
    Creates a linear order of the nodes such that u appears before v in the linear order if v depends on u (so that
    (u,v) is an edge in the graph.
    :return:
    """
    sorted_graph = []
    unsorted_graph = self.get_unsorted_graph()
    nodes = set([node for node in unsorted_graph.keys()])

    # Create dictionary: node : number of in-degrees
    in_degree = {}
    for node, edges in self.get_unsorted_graph().items():
        in_degree[node] = len(edges)

    next_node = [node for node in in_degree if in_degree[node] == 0]

    while next_node:
        current = next_node.pop(0)
        nodes.remove(current)
        sorted_graph.append(current)

        # Find all the nodes that are adjacent to current: nodes that have current in one of their edges
        for vertex in nodes:
            if current in unsorted_graph[vertex]:
                in_degree[vertex] -= 1
                if in_degree[vertex] == 0:
                    next_node.append(vertex)

    return sorted_graph
```

The following is highlighted using the Pygments highlighter native to Jekyll:
{% highlight python %}
def build_unsorted_graph(self):
    # Given the nodes, create an unsorted graph with has the list of nodes and all the vertices they are tied to

    interim = {}
    for node in self.nodes:
        # dependencies are the list of nodes that need to be started before current node is started
        # so in a graph, the dependencies would be incoming arrows that go to the current node
        if node not in interim:
            interim[node] = node.dependencies

    self.set_unsorted_graph(interim)
    return interim
{% highlight %}
