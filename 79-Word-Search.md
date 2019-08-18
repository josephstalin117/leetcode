Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

#### Example1:
```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

#### Solution
```
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        if(board.size()==0) return false;
        int h=board.size();
        int w=board[0].size();
        for(int i=0; i<w; i++)
            for(int j=0; j<h; j++)
                if(search(board, word, 0, i, j, w, h)) return true;
        return false;
    }
    
    bool search(vector<vector<char>>& board, const string& word, int d, int x, int y, int w, int h){
        if(x<0 || x==w || y<0 || y==h ||word[d]!=board[y][x]){
            return false;
        }
        
        // Found the last char of the word
        if(d==word.length()-1)
            return true;
        // 防止多次重复访问
        char cur=board[y][x];
        board[y][x]=0;
        bool found=search(board, word, d+1, x+1, y, w, h)
                    ||search(board, word, d+1, x-1, y, w, h)
                    ||search(board, word, d+1, x, y-1, w, h)
                    ||search(board, word, d+1, x, y+1, w, h);
        board[y][x]=cur;
        return found;
    }
};
```
