# 트라이  


트라이(trie)

**문자열 검색**을 빠르게 실행할 수 있도록 설계한 트리 형태의 자료구조

효율적인 정보 검색 자료구조.

M = (maximum string length 문자열의 최대 길이)

N = 찾아야 하는 문자열(키 문자열)의 개수 (key의 개수)

검색 시간  : O(M), 트리의 깊이 depth가 string 문자열의 최대 길이 이므로, 최대로 걸리는 탐색시간은  O(M) 임.

(BST, O(M*logN) 보다 빠르게 찾을 수 있다.)

장점 : 검색,insert or delete 시간이 O(M)으로 가능함.

[https://www.geeksforgeeks.org/advantages-trie-data-structure/](https://www.geeksforgeeks.org/advantages-trie-data-structure/)

단점 : storage requirements  , child 노드로 자기 자신을 가져가기 때문에 메모리 효율성이 떨어짐.

메모리를 줄여 야 할때( [ternary-search-tree](https://www.geeksforgeeks.org/ternary-search-tree/) )를 사용함

참고 : geeksforgeeks [https://www.geeksforgeeks.org/trie-insert-and-search/](https://www.geeksforgeeks.org/trie-insert-and-search/)

핵심 이론

단어들을 사전의 형태로 생성 → 트리의 부모 자식 노드 관계를 이용해 검색을 수행

```bash
// Trie node 
struct TrieNode 
{ 
     struct TrieNode *children[ALPHABET_SIZE];
     // isEndOfWord is true if the node 
     // represents end of a word 
     bool isEndOfWord; 
};
```

트라이의 특징

- N진 트리 : 문자 종류의 개수에 따라 N이 결정, 알파벳은 26진 트리
- 루트 노드 : 항상 빈 문자열을 뜻하는 공백 상태 유지

예제

[14425번: 문자열 집합](https://www.acmicpc.net/problem/14425)

## 문제

총 N개의 문자열로 이루어진 집합 S가 주어진다.

입력으로 주어지는 M개의 문자열 중에서 집합 S에 포함되어 있는 것이 총 몇 개인지 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 문자열의 개수 N과 M (1 ≤ N ≤ 10,000, 1 ≤ M ≤ 10,000)이 주어진다.

다음 N개의 줄에는 집합 S에 포함되어 있는 문자열들이 주어진다.

다음 M개의 줄에는 검사해야 하는 문자열들이 주어진다.

입력으로 주어지는 문자열은 알파벳 소문자로만 이루어져 있으며, 길이는 500을 넘지 않는다. 집합 S에 같은 문자열이 여러 번 주어지는 경우는 없다.

## 출력

첫째 줄에 M개의 문자열 중에 총 몇 개가 집합 S에 포함되어 있는지 출력한다.

문제 분석하기

---

집합 S에 속해 있는 단어들 → 트라이 구조를 생성

트라이 검색 →  문자열 M개의 포함여부를 카운트

손으로 풀어보기

---

트라이 자료구조 생성

- **현재 문자열을 가리키는 위치의 노드? (투 포인터? 이거 알아야하나?)**가 공백 → 신규 노드 생성

  → false, i++

- 문자열의 끝 → leaf node 표시 ? 어떻게?

```java
재귀로 푼다.?
인접리스트로 해결할 경우, 무한 재귀가 너무 많이 반복됨.

투포인터 현재 노드, 리프 노드!

N= 5, M=11
//ArrayList<Integer>[] tree = [26];

0 번노드 루트는 공백
tree[b] = {a} - {e} - {k} ...
tree[s] = {t} - {a} ...
         - {u} - {n} - ...
tree[c] = {o} = {d} = {e} - {p} - ...
                    - {i} - {n} - ...
            

ArrayList tree = new <>()

// current node와 leaf node를 cnt 하면 오히려 여러번 count 하게 되니까.
// 단순히 string.size()를 받아서 lengh 로 loop를 돌리고, 
// bool 타입의 leaf 면 true 를 반환하도록 변수를 두는게 낫다.
int current_node
int leaf_node

node = {current_node, next_node, ifLeaf} 로 이루어져있어야지
class Node{
Node[] next = new node[26]; // 자식노드가 멀티노드구나 최대 26개를 가질수 있어.
boolean ifLeaf = false;
}
// tree는 Node 로 구성이되어잇지.
ArrayList<Node> tree = new ArrayList<>();

tree의 깊이는 string의 lengh의 최댓값 이겟지.
알기가 어려워.

string N 개 동안 loop
i~N까지
// 첫번째 노드는 루트 노드야. 값이 없어 0
Node root;
Node now = root;

now.next 를 넣어야지.
i = 0 일때
일단 첫번째 S[0] = baekjoononelinejudge 에 대해
//그치 고급 for 쓰면 되겟네.
for( char c : S[0])

now = root, c = 'b' 일때,
now.next['b'] = true; // root -> 'b' // root.next = 'b'
now = now.next;

now = 'b', c = 'a' 일때,
now.next['a'] = true;
now = now.next;
...

now = 'g', c = 'e' 일때,
now.next['e'] = true;
now= now.next;

for 문 종료
now.ifLeaf = true;
now = root;
i++ (loop)

S[i] = codingsh 일때,

..
for(i) 종료.

int cnt=0;

for (int m = 0; m<M; m++ ) // 찾을 문자열 loop

String[] search;
now = root;
for(char c : search[m])
m=0, search[0] = baekjoon
c = 'b' 
now.next[c] 가 null 이니?
null 이면 break; 다음 문자열로
else
now.next['b'] = true 라서 넘어가,
now.next['b'];
now=now.next['b'];

c='a' 가되면,
...
c='n' 이 되면,

if (now.ifLeaf 가 true?)
	cnt++;
else 면 그냥 다음 문자열

 

tree -> current node 'b'
//current_node = 'b' 일 때,

신규 노드 추가
tree[b] = { b }
current_node++;

tree 공백이니? yes
current_node++;
tree[current_node] = { b a .. ... j u d g e}

for 종료
c 끝났어
leaf_node = current_node-1;

S[1] = star...
current_node= '1'
tree[1] = {b}
공백이니?

```

코드 구현

---

```bash
package tree.trie;

import java.io.*;
import java.util.StringTokenizer;

public class FindString {

    static int N; // 키 문자열의 개수.
    static int M; // 검사해야하는 문자열의 개수
    static int cnt=0;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken()); // 집합 S에 포함되어있는 문자열의 개수
        M = Integer.parseInt(st.nextToken()); // 검사해야 하는 문자열의 개수

        String[] S = new String[N];
        String test;

        for (int i = 0; i < N; i++) {
            S[i]=br.readLine();
        }

        TrieNode trie = InsertToTrie(S);

        for (int i = 0; i < M; i++) {
            test=br.readLine();
            SearchString(trie,test);
        }

        br.close();
        System.out.println(cnt);

    }

    static TrieNode InsertToTrie(String[] S){

        // root 노드 생성
        TrieNode root = new TrieNode();

        // 대상 key 문자열을 trie에 insert
        for(int n =0;n<N;n++){
            TrieNode node = root;
            // 각각의 문자열 S[n] 에 대하여
            for(int i=0;i<S[n].length();i++){
                char c = S[n].charAt(i);
                // S[n]의 charAt[] 에 대하여 (문자열의 철자 1개씩)
                if(node.child[c-'a']==null) { // child가 없으면
                    node.child[c-'a']=new TrieNode(); // child 추가
                }
                // 현재 node는 마지막 전 문자.
                // 현재 node의 child[c]가 마지막 문자노드
                node=node.child[c-'a']; // 자식 노드로 내려가.
                // 현재 노드가 마지막 노드,
                // 문자열의 마지막 char 일때
                if(i==S[n].length()-1) {
                    node.ifLeaf=true;
                }
            }
        }
        return root;
    }

    static void SearchString(TrieNode trie,String test){
        // test 문자열이 trie에 해당하는지 search

        for (int i=0;i<test.length();i++){
            char c = test.charAt(i);
            if(trie.child[c-'a']==null) // trie 없으면 꽝
                break;
            else {
                trie=trie.child[c-'a'];
                if(i==test.length()-1&&trie.ifLeaf==true) // test string도 마지막문자여야함.
                    cnt++;
            }
        }
    }

    static class TrieNode{
        TrieNode[] child = new TrieNode[26];
        Boolean ifLeaf=false;
    }

}
```

시간 분석

---

시간 복잡도 : O(문자열의 최대길이)

trie로 푸는 것이 해당 문제의 최단정답일 것이라 생각하였으나,

hashset 을 이용한 풀이가 가장 최단 정답으로 보임.

주어진 문제에서 key 문자열이 중복되지 않기때문에 → set으로 넣어서 구성하여도 될것으로 보인다.

아니면, 문자열의 판단을 String 클래스를 사용하는 것이 아니라

byte 연산을 해서 그런것인가?

문자를 비교하는 byte 연산 하는법 추후에 다시 해서 문제 다시 풀어보자.