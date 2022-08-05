```c++
#include<stack>

bool isValidParenthesis(string expression)
{
    stack<char> st;
    
    for(auto x: expression){
        
        if(x == '(' || x == '{' || x == '[')
            st.push(x);
        else{
            if(st.size() == 0) // "]()"
                return false;
            else{
                char topp = st.top();
                st.pop();
                if((topp == '(' && x == ')') || (topp == '[' && x == ']') ||( topp == '{' && x == '}'))
                    continue;
                else
                    return false;
            }
        }
    }
    if(st.empty())
        return true;
    else
        return false;
}
```
