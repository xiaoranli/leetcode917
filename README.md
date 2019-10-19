# 15、leetcode917. 仅仅反转字母
解法一：
--  
思路：
--
    双指针，分别从字符串前后开始向中间移动，如果不是字符或数字则跳过，如果都是则交换。    
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/19 16:41
 * @descriptor  917. 仅仅反转字母
 */
public class ReverseOnlyLetters_917 {
    public static String reverseOnlyLetters(String s) {
        char[] c = s.toCharArray();
        int i = 0,j = c.length-1;
        while(i < j){
            if(valid(c[i]) && valid(c[j])){
                swap(c,i,j);
                i++;
                j--;
            }else if(!valid(c[i]))
                i++;
            else if(!valid(c[j]))
                j--;
        }
        return new String(c);
    }
    private static void swap(char[] c, int i, int j) {
        char temp = c[i];
        c[i] = c[j];
        c[j] = temp;
    }
    private static boolean valid(char c) {
        if((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z'))
            return true;
        else
            return false;
    }
    public static void main(String[] args) {
        String s = "a-bC-dEf-ghIj";//"j-Ih-gfE-dCba"
        String s1 = reverseOnlyLetters2(s);
        System.out.println(s1);
    }
}
</pre>
解法二：
--  
思路：
--
    栈。将 s 中的所有字母入栈，所以出栈等价于对字母反序操作。然后，遍历 s 的所有字符，如果是字母我们就选择栈顶元素输出。  
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/19 16:41
 * @descriptor  917. 仅仅反转字母
 */
public class ReverseOnlyLetters_917 {
    public static String reverseOnlyLetters2(String s) {
        Stack<Character> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            if(Character.isLetter(s.charAt(i))) {
                stack.push(s.charAt(i));
            }
        }
        StringBuilder builder = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            if(Character.isLetter(s.charAt(i))){
                builder.append(stack.pop());
            }else{
                builder.append(s.charAt(i));
            }
        }
        return builder.toString();
    }
    public static void main(String[] args) {
        String s = "a-bC-dEf-ghIj";//"j-Ih-gfE-dCba"
        String s1 = reverseOnlyLetters2(s);
        System.out.println(s1);
    }
}
</pre>
解法三：
--  
思路：
--
    维护一个StringBuilder，不再使用前后字符交换的思路。维护一个指针 j 从后往前遍历字符串，当需要字母时就使用它。  
--
<pre>
/**
 * @author lihe
 * @date 2019/10/19 16:41
 * @descriptor  917. 仅仅反转字母
 */
public class ReverseOnlyLetters_917 {
    public static String reverseOnlyLetters1(String s) {
        StringBuilder builder = new StringBuilder();
        int j = s.length() - 1;
        for (int i = 0; i < s.length(); i++) {
            if(Character.isLetter(s.charAt(i))){
                while(!Character.isLetter(s.charAt(j))){
                    j--;
                }
                builder.append(s.charAt(j--));
            }else{
                builder.append(s.charAt(i));
            }
        }
        return builder.toString();
    }
    public static void main(String[] args) {
        String s = "a-bC-dEf-ghIj";//"j-Ih-gfE-dCba"
        String s1 = reverseOnlyLetters2(s);
        System.out.println(s1);
    }
}
</pre>
