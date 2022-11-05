# C++のfilesystem

おそらく使わないであろうfilesystemだけど、一応残す

library-descriptionの開発で作ったけど最終的には使わなかったcode-replace.cpp

ほんとは実行時のコマンドライン引数でファイルパスを渡すやつだった

```cpp
// g++ -std=c++1z -lstdc++ -lstdc++fs code-replace.cpp
// ./a.out
// example
// @assets/Library/graph/dijkstra.cpp@ (in articles/dijkstra.md) -> [code in dijkstra.cpp]
#include <filesystem>
#include <fstream>
#include <string>
#include <vector>
#include <iostream>

using std::endl;
using std::string;
using std::vector;

const char target = '@';

struct file {
  vector<string> lines;
  string path;
  std::ifstream fin;
  std::ofstream fout;
};


vector<string> inputFileText(std::ifstream &fin){
  vector<string> lines;
  string line;

  while(getline(fin, line)){
    lines.emplace_back(line);
  }
  return lines;
}

string findBetweenText(const vector<string> &lines){
  bool found = false;
  string between_text;

  for(const string &line : lines){
    for(char c : line){
      if(found){
        if(c == target) return between_text;
        between_text += c;
      }else{
        if(c == target) found=true;
      }
    }
  }
  return "not find!";
}

void replaceText(vector<string> &lines,const vector<string> &insert_text){
  int i=0;
  for(string line : lines){
    if(line.find(target) == string::npos){
      i++;
      continue;
    }

    lines.erase(lines.begin() + i);

    int j=0;
    for(string text : insert_text){
      lines.insert(lines.begin() + i + j, text);
      j++;
    }

    break;
  }
}

int main(){
  for(const std::filesystem::directory_entry &i:std::filesystem::recursive_directory_iterator("./content/articles/")){
    file md, cpp;


    // get markdown file path
    md.path=i.path().string();


    // open markdown file for input
    md.fin.open(md.path);
    if(!md.fin.is_open()) continue;


    // input lines
    md.lines = inputFileText(md.fin);


    // find $hogehoge$
    cpp.path = findBetweenText(md.lines);


    // open cpp file in library
    cpp.fin.open(cpp.path);
    if(!cpp.fin.is_open()) continue;


    // input code
    cpp.lines = inputFileText(cpp.fin);


    // replace $hoge$ -> [code]
    replaceText(md.lines,cpp.lines);


    // close file
    md.fin.close();
    cpp.fin.close();


    // open markdown file for output
    md.fout.open(md.path);
    if(!md.fout.is_open()) continue;
    

    // overwrite markdown file
    for(const string line : md.lines){
      md.fout << line << '\n';
    }
  }

  return 0;
}

```



### filesystemの何がすごいか

- 再帰が簡単
- 分かりやすい
- c++だから日本語公式リファレンスも記事もある

### filesystemの何が不満か

- コンパイルするときに謎のオプションがある
- インテリジェンスがfilesystemの関数に赤線を出してしまう



