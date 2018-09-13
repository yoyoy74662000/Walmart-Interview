# Walmart-Interview
Java, Algorithm

[1 twosum] [38.8%	Easy]使用 HashMap✅
```java
 public int[] twoSum(int[] nums, int target) {
        if(nums == null || nums.length == 0) return null;
        int[] res = new int[2];
        HashMap<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            if(map.containsKey(target - nums[i])){
                res[0] = map.get(target - nums[i])  ;
                res[1] = i;
            }else{
                map.put(nums[i], i);
            }
        }
        return res;
 }
```

[3 Longest Substring Without Repeating Characters] [25.0%	Medium]使用 HashSet, HashMap✅
```java
 public int lengthOfLongestSubstring(String s) {
        if(s == null || s.length() == 0) return 0;
        HashMap<Character, Integer> map = new HashMap<>();
        int res = 0;
        for(int i = 0, j = 0; i < s.length(); i++){
            if(map.containsKey(s.charAt(i))){
                j = Math.max(j, map.get(s.charAt(i)) + 1);
            }
            map.put(s.charAt(i), i);
            res = Math.max(res, i - j + 1);
            
        }
        return res;
}
```

[4 Median of Two Sorted Arrays] [23.8% Hard] 先merge兩個array，再去算中位數✅
```java
 public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int i = 0, nums1Size = nums1.length;  //  setting pointer for first array
        int j = 0, nums2Size = nums2.length;    //  setting pointer for second array
        int total = nums1Size + nums2Size;   //  getting total elements in both arrays

        int mergeds1s2[] = new int[total];  //  new array to store sorted elemented
        int k=0;

        //  merging both arrays into mergeds1s2 to get the final sorted array
        while(i<nums1Size && j<nums2Size) {

            if(nums1[i] < nums2[j]) mergeds1s2[k] = nums1[i++];
            else mergeds1s2[k] = nums2[j++];
            k++;
        }

        if(i==nums1Size){
            while (j<nums2Size) mergeds1s2[k++] = nums2[j++];
        }
        else {
            while (i<nums1Size) mergeds1s2[k++] = nums1[i++];
        }

        //  returning the median.
        if(k%2 == 1) {
            return mergeds1s2[k/2];
        }
        else{
            return (mergeds1s2[k/2]+mergeds1s2[k/2 - 1])/2.0;
        }
    }
```

[5 Longest Palindromic Substring] [25.0% Medium]使用一個helper left-- right++類似中心擴散出去✅
```java
 String res = "";
    public String longestPalindrome(String s) {
        if(s == null || s.length() ==0) return res;
        for(int i = 0; i < s.length(); i++){
            helper(s, i, i);
            helper(s, i, i+1);
        }
        return res;
    }
    
    public void helper(String s, int left, int right){
        while(left >= 0 && right < s.length() && s.charAt(left)==s.charAt(right)){
            left--;
            right++;
        }
        String cur = s.substring(left + 1, right);
        if(cur.length() > res.length()){
            res = cur;
        }
        
    }
```
[11 Container With Most Water] [38.5% Medium] 底*math.min高✅
```java
public int maxArea(int[] height) {
        if(height == null || height.length == 0) return 0;
        int start = 0, end = height.length -1;
        int max = 0;
        while(start < end){
            // 高度要找最小的
            max = Math.max(max, (end - start) * Math.min(height[start], height[end]));
            if(height[start] > height[end]){
                end--;
            }else{
                start++;
            }
        }
        return max;
    }
```

[21 Merge Two Sorted Lists] [43.0% Easy]使用一個helper 最還要注意 if(p ==null) else✅
```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null && l2 == null) return null;
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        cur.next = merge(l1, l2);
        return dummy.next;
    }

    public static ListNode merge(ListNode l1, ListNode l2){
        ListNode p = l1, q = l2;
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;

        while(p != null && q != null){
            if(p.val <= q.val){
                cur.next = new ListNode(p.val);
                p = p.next;
                cur = cur.next;
            }else{
                cur.next = new ListNode(q.val);
                q = q.next;
                cur = cur.next;
            }
        }
        if(p == null){
            cur.next = q;
        }else{
            cur.next = p;
        }
        return dummy.next;
    }
```
[22 Generate Parentheses] [50.0%	Medium] backtracking✅
```java
public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();    
        String s = "";
        helper(res, s, n, n);
        return res;
    }
    
    public void helper(List<String> res, String s, int left, int right){
        if(left > right){
            return;
        }
        if(left == 0 && right == 0){
            res.add(s);
        }
        if(left > 0){
            helper(res, s + '(', left -1, right);
        }
        if(right > 0){
            helper(res, s + ')', left, right-1);
        }
    }
```

[26 Remove Duplicates from Sorted Array] [37.7%	Easy]爛題目✅
```java
 public int removeDuplicates(int[] nums) {
        if(nums == null) return 0;
        int count = 1;
        for(int i = 1; i < nums.length; i++){
            if(nums[i] != nums[i-1]){
                nums[count++] = nums[i];
            }
        }
        return count;
    }
```

[46 Permutations] [49.7% Medium]使用 backtracking helper✅
```java
public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> list = new ArrayList<>();
        if(nums == null || nums.length == 0) return res;
        helper(res, list, nums);
        return res;
    }

    public static void helper(List<List<Integer>> res, List<Integer> list, int[] nums){
        if(list.size() == nums.length){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i = 0; i < nums.length; i++){
            if(list.contains(nums[i])) continue;
            list.add(nums[i]);
            helper(res, list, nums);
            list.remove(list.size() - 1);
        }


    }
```

[49 Group Anagrams] [49.7% Medium]使用 HashMap來記錄，再來sort string 放到 HashMap✅
```java
public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> res = new ArrayList<>();
        if (strs == null || strs.length == 0) return res;
        HashMap<String, Integer> map = new HashMap<>();
        for (String str : strs ){
            char[] ch = str.toCharArray();
            Arrays.sort(ch);
            String s = new String(ch);
            if (map.containsKey(s)){
                // res.get 是指 get ArrayList index 位置
                res.get(map.get(s)-1).add(str);
            }else{
                List<String> list = new ArrayList<>();
                list.add(str);
                res.add(list);
                map.put(s,res.size());
            }
        }
        return res;

    }
```
[54 Spiral Matrix] [28.1%	Medium] 背起來✅
```java
public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<>();
        if (matrix == null || matrix.length == 0 || matrix[0] == null || matrix[0].length == 0) {
            return res;
        }
        
        int rowbegin = 0;
        int rowend = matrix.length -1;
        int colbegin = 0;
        int colend = matrix[0].length -1;
        

        while (rowbegin <= rowend && colbegin <= colend) {
            for (int i = colbegin; i <= colend; i++) {
                res.add(matrix[rowbegin][i]);
            }
            rowbegin++;

            for (int i = rowbegin; i <= rowend; i++) {
                res.add(matrix[i][colend]);
            }
            colend--;

            if (rowbegin <= rowend) {
                for (int i = colend; i >= colbegin; i--) {
                    res.add(matrix[rowend][i]);
                }
            }
            rowend--;

            if (colbegin <= colend) {
                for (int i = rowend; i >= rowbegin; i--) {
                    res.add(matrix[i][colbegin]);
                }
            }
            colbegin++;
        }

        return res;
    }
```
[56. Merge Intervals] [32.9%	Medium]背起來✅
```java
public List<Interval> merge(List<Interval> intervals) {
        // sort start&end
        int n = intervals.size();
        int[] starts = new int[n];
        int[] ends = new int[n];
        for (int i = 0; i < n; i++) {
            starts[i] = intervals.get(i).start;
            ends[i] = intervals.get(i).end;
        }
        Arrays.sort(starts);
        Arrays.sort(ends);
        // loop through
        List<Interval> res = new ArrayList<Interval>();
        for (int i = 0, j = 0; i < n; i++) { // j is start of interval.
            if (i == n - 1 || starts[i + 1] > ends[i]) {
                res.add(new Interval(starts[j], ends[i]));
                j = i + 1;
            }
        }
        return res;
    }
```
[62 Unique Paths] [44.2%	Medium]使用 DP 邊上 相加✅
```java
public int uniquePaths(int m, int n) {
        int[][] res = new int[m][n];
        
        for(int i = 0; i < m; i++){
            res[i][0] = 1;
        }
        
        for(int j = 0; j < n; j++){
            res[0][j] = 1;
        }
        
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                res[i][j] = res[i-1][j] + res[i][j-1];
            }
        }
        return res[m-1][n-1];
    }
```

[70 Climbing Stairs] [42.0%	Easy]使用 DP mem[i] = mem[i-1] + mem[i-2]✅
```java
public int climbStairs(int n) {
        if(n == 0 || n == 1 || n == 2){
            return n;
        }
        int[] mem = new int[n];
        mem[0] = 1;
        mem[1] = 2;
        for(int i = 2; i < n; i++){
            mem[i] = mem[i-1] + mem[i-2];
        }
        return mem[n-1];
    }
```
[79 Word Search] [28.9%	Medium]請記住 backtracking✅
```java
public boolean exist(char[][] board, String word) {
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[0].length; j++){
                //找第一個起始值
                if(exist(board, word, i, j, 0)){
                    return true;
                }
            }
        }
        return false;
    }

    private boolean exist(char[][] board, String word, int i, int j, int start){
        if(start >= word.length()) return true;
        if(i < 0 || i >= board.length || j < 0 || j >= board[0].length) return false;
        if(board[i][j] == word.charAt(start++)){
            char c = board[i][j];
            board[i][j] = '#';
            boolean res = exist(board, word, i + 1, j, start) ||
                          exist(board, word, i - 1, j, start) ||
                          exist(board, word, i, j + 1, start) ||
                          exist(board, word, i, j - 1, start);
            board[i][j] = c;
            return res;
        }else {
            return false;
        }
    }
```
[92. Reverse Linked List II] [31.6%	Medium]使用dummy 記住 temp prev cur 使用方式✅
```java
public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next =head;
        ListNode cur = dummy.next;
        ListNode prev = dummy;
        for(int i = 1; i < m; i++){
            cur = cur.next;
            prev = prev.next;
        }
        for(int i = 0; i < n - m; i++){
            ListNode temp = cur.next;
            cur.next = temp.next;
            temp.next = prev.next;
            prev.next = temp;
        }
        return dummy.next;
    }
```

[138 Copy List with Random Pointer] [31.6%	Medium]請記住 HashMap✅
```java
public RandomListNode copyRandomList(RandomListNode head) {
        HashMap<RandomListNode, RandomListNode> map = new HashMap<>();
        RandomListNode cur = head;
        while(cur != null){
            map.put(cur, new RandomListNode(cur.label));
            cur = cur.next;
        }
        cur = head;
        while(cur != null){
            map.get(cur).next = map.get(cur.next);
            map.get(cur).random = map.get(cur.random);
            cur = cur.next;
        }
        return map.get(head);
    }
```

[148 Sort List] [31.6%	Medium]請記住 取mid 再 merge✅
```java
public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode mid = getmid(head);
        ListNode next = mid.next;
        mid.next = null;
        return merge(sortList(head), sortList(next));
    }

    public static ListNode getmid(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    public static ListNode merge(ListNode a, ListNode b) {
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        while (a != null && b != null) {
            if (a.val <= b.val) {
                cur.next = a;
                a = a.next;
            } else {
                cur.next = b;
                b = b.next;
            }
            cur = cur.next;
        }
        if (a == null) cur.next = b;
        else cur.next = a;
        return dummy.next;
    }
```

[153 Find Minimum in Rotated Sorted Array] [41.5%	Medium]請記住 binary search✅
```java
public int findMin(int[] nums) {
        if(nums.length == 0) return -1;
        int start = 0;
        int end = nums.length -1;
        while(start + 1 < end){
            int mid = (end - start) / 2 + start;
            if(nums[mid] < nums[end]){
                end = mid;
            }else{ // [1,3,3] 類似有重複
                start = mid;
            }
        }
        if(nums[start] < nums[end]) return nums[start];
        else return nums[end];
}
```

[自創 Find Maximum in Rotated Sorted Array] [41.5%	Medium]請記住 binary search✅
```java
public static void main(String[] args) {
        int[] array = {4,5,6,1,2,3};
        System.out.println(findMin(array));
    }

    public static int findMin(int[] nums) {
        if(nums.length == 0) return -1;
        int start = 0;
        int end = nums.length -1;
        while(start + 1 < end){
            int mid = (end - start) / 2 + start;
            if(nums[start] > nums[mid]){
                end = mid;
            }else{ // [1,3,3] 類似有重複
                start = mid;
            }
        }
        if(nums[start] > nums[end]) return nums[start];
        else return nums[end];
    }
```
[203 Remove Linked List Elements] [49.1% Easy]使用 dummy✅
```java
public ListNode removeElements(ListNode head, int val) {
        if(head == null) return null;
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode cur = dummy;
        while(cur.next != null){
            if(cur.next.val == val){
                cur.next = cur.next.next;
            }else{
                cur = cur.next;
            }
        }
        return dummy.next;
    }
```
[206 Reverse Linked List] [49.1% Easy]使用 prev temp head✅
```java
public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        if (head == null || head.next == null) return head;
        while(head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        return prev;
    }
```

[214 Shortest Palindrome] [25.8% Hard]背下來 return new StringBuilder(s.substring(end+1)).reverse().toString()+s;✅
```java
public String shortestPalindrome(String s) {
        int i = 0;
        int end = s.length()-1;
        int j = s.length()-1;
        while(i < j){
            if(s.charAt(i) == s.charAt(j)){
                i++;
                j--;
            }else{
                i = 0;
                end--;
                j = end;
            }
        }
        return new StringBuilder(s.substring(end+1)).reverse().toString()+s;
    }
```

[230 Kth Smallest Element in a BST] [47.2% Medium]使用 HashMap✅
```java
private int count = 0, res = 0;
    public int kthSmallest(TreeNode root, int k) {
        count = k;
        helper(root);
        return res;
    }

    public void helper(TreeNode root){
        if(root == null) return;
        helper(root.left);
        count--;
        if(count == 0){
            res = root.val;
        }
        helper(root.right);
    }
```

[232 Implement Queue using Stacks] [39.5% Easy]使用 兩個stack✅
```java
public class ImplementQueueusingStacks {
    Stack<Integer> s1 = new Stack<>();
    Stack<Integer> s2 = new Stack<>();

    public void push(int x) {

        s1.push(x);
    }

    public int pop() {
        if(!s2.isEmpty()) {
            return s2.pop();
        }
        else{
            while(!s1.isEmpty()){
                s2.push(s1.pop());
            }
            return s2.pop();
        }
    }

    public int peek() {
        if(!s2.isEmpty()) return s2.peek();
        else{
            while(!s1.isEmpty()){
                s2.push(s1.pop());
            }
            return s2.peek();
        }
    }

    public boolean empty() {

        return s1.isEmpty() && s2.isEmpty();
    }
}
```
[236 Lowest Common Ancestor of a Binary Tree] [31.6% Medium]使用 recursion✅
```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
         if (left != null && right != null){
            return root;
        }
        else {
            return left == null ? right : left;
        }
    }
```

[283 Move Zeroes] [52.3% Easy]使用 nums[start++]✅
```java
public void moveZeroes(int[] nums) {
        int start = 0;
        if(nums == null || nums.length == 0) return;
        for(int  i = 0; i < nums.length; i++){
            if(nums[i] != 0){
                nums[start] = nums[i];
                start++;
            }
        }
        while(start < nums.length){
            nums[start++] = 0;
        }
    }
```

[344 Reverse String] [61.3%	Easy]使用 swap，記得 left++ right--✅
```java
public String reverseString(String s) {
        if(s == null || s.length() == 0) return"";

        return swap(s);
    }

    public String swap(String s){
        char[] r = s.toCharArray();
        int right = s.length()-1;
        for(int left = 0; left < s.length()/2; left++){
            char temp = r[left];
            r[left] = r[right];
            r[right] = temp;
            right--;
        }
        return String.valueOf(r);
    }
```
[406 Longest Palindrome] [46.3%	Easy]使用 HashSet 注意 return 那邊 基偶問題✅
```java
public int longestPalindrome(String s) {
        if(s == null || s.length() == 0) return 0;
        int count = 0;
        HashSet<Character> set = new HashSet<>();
        for(char c : s.toCharArray()){
            if(set.contains(c)){
                set.remove(c);
                count++;
            }else{
                set.add(c);
            }
        }
        if(set.size() != 0){
            return count*2 + 1;
        }else{
            return count*2;
        }
    }
```
[add two numbers without using +] 
```java
 while(y!=0){
    int carry = x & y; 
    x = x^y; 
    y = carry << 1;
 } 
 return x;
```
