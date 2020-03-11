## Q1 [Array]. ACompare arrays

Give two arrays $a and $b of integers, write a function checkEquals() that check if two arrays contain same values.

```
function checkEquals($a,$b); // Return boolean
```

Example:

```
checkEquals([1,2,3], [3,1,2]); // Return true
checkEquals([1,2,5,2], [5,2,1,2]); // Return true
checkEquals([1,2,5,2], [5,2,1]); // Return false
```

What is the running time of the algorithm?


## Q2 [String]. Normalize string

Give a string `$str`, write a function to `normalize` it, i.e, remove all consecutive spaces & newlines and spaces &new lines at two ends.

```
// Return a new string with all multiple spaces removed, spaces at two ends remove 
function normalize($str);
```

Example:

```
normalize(" ab    cdef g "); // Return "ab cdef g"
```

## Q3 [Randomization]. Randomize an array of n elements
Give a number `$n`, construct a TRUE random array of exactly `n` different elements from `1` to `n`. True random means that all possiblities could be created with same probability.

```
function randomN($n); // Return a random array
```

Example:

```
randomN(4); // May return [1,3,2,4]
randomN(6); // May return [6,1,5,2,4,3]
```


## Q4 [Security]. Web security

Alice is a web programmer newbie, and her task is to write a simple CRUD program. She is taught that user input may contain dangerous characters and she must handle it carefuly on the server. Luckily, she find out that there is a function `base64_encode`, which encodes EVERYTHING into good characters.

Let's simplify as follow: Assume that she is given two safe functions:

```
saveToDB(mixed $id, $name); // Safely save the name of an object corresponding to an ID.
getFromDB(mixed $id); // Safely getting the object with $id from the database
```

Her backend is as follow:

```
$id = $_POST["id"];
$content = $_POST["content"];

if (!is_int($id)){
	exit;
}

saveToDB($id, base64_encode($content));

```

And the frontend is simple, too:

```

<?php 
	$id=$_GET["id"];
    if (!is_int($id)){
    	exit;
    }
    
	$obj = getFromDB($id); 
    if (!$obj){
    	exit;
    }
?>

<form method='POST' action ='https://mywebsite.com/save'>
	<input name='id' value='<?php echo $obj->id; ?>'/>
    <textarea name='name'><?php echo base64_decode($obj->content); ?></textarea>
</form>
```

What's wrong with the above code?


## Q5 [OOP]. Tree API

You need to implement the following tree interface:

```
interface TreeInterface{
	public function init(stdClass[] $array);
    public function getNode(int $id);
    public function getNodes(int $id): Node[];
    public function getParent(int $id): Node;
    public function toString(); // Print nested <ul, li>
}
```
Here is what you need to implement, and feel free to add any constructor, variables, extra functions when needed.

```
class Node{
	int $id;
    int $parent_id;
    int $name;
}

class Tree implements TreeInterface{
	... YOUR CODE HERE ...
}
```

**Explain**: Each Tree will contain many nodes, whereas `node.parent_id=0` means this node is connected to the tree root. The init function may be called as follow:

```
// Here I use javascript shorthand, the code is not VALID PHP code but you should understand it
$direct_nodes = [{id: 1, name: "Node A", parent_id: 0}, {id: 2, name: "Node B", parent_id: 0}, {id: 1, name: "Node A1", parent_id: 1}, {id: 1, name: "Node A2", parent_id: 1}]; 

$tree=new Tree();
$tree->init($direct_nodes);
```

In this case, `$tree->toString()` should output:

```
<ul><li>A<ul><li>A1</li><li>A2</li></ul></li><li>B</li></ul>
```

and `$tree->get(2)` should return some object like `{id: 2, name: "Node B", parent_id: 0}`.

You need to explain the running time of the above functions.



## Q6 [OOP/JS]. Implement Q5 but in Javascript

Also explain the running time of the algorithm.
