## Interview Feedback
0. ***Think through your solution before presenting in interview.*** 
1. Don’t ask if interviewer can give more examples. Instead, you give an example and check with interviewer on your questions.
2. Don’t ask interviewer for time complexity restraint. Instead, you should propose your brute force method solution (and say this is brute force).
3. Don’t ask interviewer for function signature. You should write something and check with interviewer if it is okay.
4. When you are explaining your brute force, don’t just say the time complexity and assume interviewer will understand what you are talking about. You should just     
   explain your brute force solution clearly. If you are having difficulty explaining your idea clearly, use an example.
5. Instead of writing an if statement or thinking to words to describe the element in the array you re iterating over, just explain that you for loop through the given   
   array and did “something” each iteration.
6. Don’t say stupid in interview.
7. When you are explaining your solution, you should highlight the part of the code you are explaining.
8. When you go through example, if there are a lot of variables, try to write down the values as you go.
9. Ran over interview 8min.
10.keep asking questions.
## Coding Style
1. While(only the boundary constrains here)
2. Don’t put too much items in a loop(for/while/foreach)
3. If a part of code will be reused, put it into a single method and everytime when you call this method;
4. Bug free, which means before you run your code, you should check whether some cases will make your code crashed.
## Normal used syntax/reference
1. using System.Collections.Generic;
2. using System.Text;
3. using System.linq;
## C# Methods/Properties/functions
 ```C#
 //Array
 int[][] cache = new int[row][];
 for(int i = 0; i < row; i++)
 {
    cache[i] = new int[col];
 }
 int[][] res = new int[][]{};
 list.ToArray();//list to Array
 int[,] directions = new int[,]{{1,0},{-1,0},{0,1},{0,-1}};
 int new_row = cur.Item1 + directions[i,0];//cur is a tuple
 int[][] sorted = intervals.OrderBy(x =>x[0]).ToArray();
 int[][] ranks = dict.OrderByDescending(o => o.Value).Select(o => new int[]{o.Key,o.Value}).ToArray();
 
 
 //String StringBuilder
 StringBuilder sb = new StringBuilder();
 sb.Append("Hello");
 sb.Append('a');
 sb.Insert(5,"CACVD"); //inserts a string/char at the specified index in the StringBuilder object.
 sb.Insert(5,'a');
 sb.Remove(sb.Length - 1,1);//remove a string from the specified index and up to the specified length.
 
 string s = new string();
 s.ToLower();s.ToUpper();
 s.Trim();
 (s[i] > 'a' && s[i] < 'z') || (s[i] > '0' && s[i] < '9') // Printable ASCII character
 "abc" == "abc" //value equal
 s.Equals(s); //object equal
 new string(c); //charArray to string
 string.split(); //returns a string array
 string authorName = bio.Substring(0, 12); // Get first 12 characters substring from index 0; 
 string authorBio = bio.Substring(12);  // Get everything else after 12th position (start from 1st position which is index 0) 

 
 
 //List
 list.AddRange();//add all items from another list.
 IList<IList<int>> res = new List<IList<int>>();
 res.Add(new List<int>{1,2,3});
 list.Remove(...);//O(N)
 list.RemoveAt(index);//if the index is the last one, then O(1), otherwide O(N);
 
 string[] animals = { "Cow", "Camel", "Elephant" };
 List<string> animalsList = new List<string>(animals);//array => list
 
 
 //Int
 Int32.MaxValue/Int32.MinValue
 
 
 //HashMap
 dic.Remove(lruList.Last.Value);
 lruList.RemoveLast();
 dic.Add(key,value);
 lruList.AddFirst(key);    // LRU cache
 int key = dict.Where(o => o.Value == operation[0]).Select(o => o.Key).FirstOrDefault(); //Enumerate int to int

 
 
 //Char
 for(char c = ‘a’; c <= ‘z’;c++){…}//word ladder
 char foo = '2'; int bar = foo - '0'; //convert char to int (if you use convert.T0Int32, it will return the asicc number)
 IP.IndexOf('.') != -1  //determine whether exist '.' In it

 
 //Heap(Priority Queue)
 PriorityQueue<int,int> pq = new PriorityQueue<int, int>(); //pop out the smallest priority value
 PriorityQueue<int,int> pq = new PriorityQueue<int,int>(Comparer<int>.Create((x,y) => y.CompareTo(x))); //pop out the largest priority value
 ```
## Templates
**Topological Sorting**
```C#
    public bool CanFinish(int numCourses, int[][] prerequisites) {
        if(prerequisites.Length == 0)
        {
            return true;
        }
        int[] degree = new int[numCourses];
        var edges = new List<int>[numCourses];
        for(int i = 0; i < numCourses; i++)
        {
           edges[i] = new List<int>();
        }
        foreach(int[] prereq in prerequisites)
        {
            ++degree[prereq[0]];
            edges[prereq[1]].Add(prereq[0]);
        }
        Queue<int> queue = new Queue<int>();
        for(int i = 0; i < degree.Length; i++)
        {
            if(degree[i] == 0)
            {
                queue.Enqueue(i);
            }
        }
        int count = 0;
        while(queue.Count != 0)
        {
            int cur = queue.Dequeue();
            ++count;
            List<int> edge = edges[cur];
            foreach(int i in edge)
            {
                --degree[i];
                if(degree[i] == 0)
                {
                    queue.Enqueue(i);
                }
            }
        }
        return count == numCourses;
    }
```
**normal BFS**
```C#
      public int LadderLength(string beginWord, string endWord, IList<string> wordList){
        if(beginWord.Equals(endWord))
        {
            return 1;
        }
        HashSet<string> set1 = new HashSet<string>();
        foreach(string s in wordList)
        {
            set1.Add(s);
        }
        HashSet<string> set2 = new HashSet<string>();
        Queue<string> queue = new Queue<string>();
        set2.Add(beginWord);
        queue.Enqueue(beginWord);
        int result = 1;
        while(queue.Count != 0)
        {
            ++result;
            int size = queue.Count;
            for(int i = 0; i < size; i++)
            {
                string temp = queue.Dequeue();
                foreach(string s in GetNextWord(temp,set1))
                {
                    if(s.Equals(endWord))
                    {
                        return result;
                    }
                    if(set2.Contains(s))
                    {
                        continue;
                    }
                    
                    set2.Add(s);
                    queue.Enqueue(s);
                }
            }
        }
        return 0;
     }
```
**Binary Search**
```C#
    public int PickIndex() {
        Random random = new Random();
        double target = totalSum * random.NextDouble();
        int left  = 0;
        int right = sum.Length - 1;
        while(left + 1 < right)
        {
            int mid = left + (right - left) / 2;
            if(target > sum[mid])
            {
                left = mid;
            }
            else if(target < sum[mid])
            {
                right = mid;
            }
            else
            {
                return mid;
            }
         }
        if(sum[left] > target)
        {
            return left;
        }
        if(sum[right] > target)
        {
            return right;
        }
        return -1;
    }
```
## Commonly Used Algorithm/Data Structure Details
