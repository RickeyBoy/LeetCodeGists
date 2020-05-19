
### Palindrome

```cpp
bool isPalin(string s) {
    if(s.size()<=1) return true;
    for(int i=0;i<s.size()/2;i++) {
        if(s.at(i)!=s.at(s.size()-1-i)) return false;
    }
    return true;
}
```

