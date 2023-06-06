# 인덱스(Index)

# Basic concepts

**Indexing**: 원하는 data에 빠르게 접근하기 위한 기술

- **record** : **index entry** 라고도 하며 특정 entitiy에 속한 filed들의 group이다.
- **Search Key** : record를 찾기 위해 사용되는 attribute
- **Index file** : record로 구성되며, 구조는  [search key][pointer]
- **Ordered indices** : 정렬된 순서로 search key가 저장
- **Hash indices** : ’hash function’을 통해 search key가 균등하게 분포되어 ‘bucket’의 주소를 가리킴

## Indexing vs Hashing

인덱스와 해싱 모두 데이터베이스에서 데이터 검색 속도를 높이는 중요한 메커니즘이지만, 둘 사이에는 몇 가지 주요한 차이점이 있다.

1. **데이터 구조**: 인덱스는 트리 기반의 데이터 구조 (예를 들어 B-Tree, B+ Tree)를 사용하여 데이터를 저장한다. 이는 데이터를 정렬된 순서로 유지하므로 범위 쿼리에 매우 효과적이다. 반면에 해시는 키를 해시 함수에 통과시켜 생성된 해시 값을 이용한다. 이 해시 값은 데이터 항목을 찾는 데 사용되며, 이는 빠른 검색을 가능하게 한다. 그러나 해싱은 순서를 유지하지 않기 때문에 범위 쿼리에 비효율적이다.
2. **속도**: 해싱은 일반적으로 키-값 쌍을 바탕으로 O(1)의 시간 복잡도로 특정 데이터를 검색할 수 있어서 매우 빠르다고 할 수 있다. 반면에 인덱스는 일반적으로 로그 시간 복잡도를 가지므로 큰 데이터 세트에서는 해싱보다 상대적으로 느릴 수 있다.
3. **중복**: 인덱스는 중복 값을 허용하지만, 해시 테이블에서는 같은 해시 값을 가지는 중복 키가 문제가 될 수 있다. 이를 '해시 충돌'이라 하며, 이를 해결하기 위한 별도의 메커니즘이 필요하다.
4. **용도**: 인덱싱은 정렬된 데이터를 저장하고 관리하며, 데이터베이스의 조인 연산, 정렬 연산에 효율적이다. 반면에 해싱은 특정 키를 통해 빠르게 데이터를 찾는 것에 최적화되어 있다.

요약하자면, 인덱스와 해싱 모두 데이터 검색 속도를 향상시키는 데 사용되지만, 구현 방식과 사용 사례에 따라 선호되는 경우가 다르다. **범위 쿼리나 정렬된 데이터가 필요한 경우에는 인덱스를, 특정 키를 통해 데이터를 빠르게 찾아야 하는 경우에는 해싱을 사용하는 것이 바람직하다.**

## key vs index

데이터베이스에서 '키(Key)'와 '인덱스(Index)'는 비슷하게 들릴 수 있지만, 역할과 용도는 다르다.

1. **키(Key)**: 키는 데이터베이스 테이블의 레코드를 고유하게 식별하거나, 레코드 간의 관계를 정의하는 데 사용되는 필드 또는 필드의 조합이다. 예를 들어, 주민등록번호, 학번 등은 고유한 식별자 역할을 하는 키가 될 수 있다. 이와 같은 키를 '기본 키(Primary Key)'라고 하며, 테이블의 각 레코드를 고유하게 식별한다. 또한 '외래 키(Foreign Key)'는 다른 테이블의 레코드와 관계를 정의하는데 사용된다.
2. **인덱스(Index)**: 인덱스는 데이터베이스에서 데이터를 더 빠르게 검색하고 접근할 수 있도록 돕는 데이터 구조다. 책의 색인과 유사하게, 데이터베이스의 인덱스는 특정 필드에 대한 포인터 또는 참조를 제공하여 해당 데이터를 더 빠르게 찾을 수 있게 한다. 인덱스는 특정 키 또는 키의 조합에 대해 생성될 수 있으며, 이 키는 인덱스를 구성하는 필드가 된다.

따라서, 키는 데이터의 고유성과 레코드 간의 관계를 보장하는 반면, 인덱스는 검색 속도와 성능 최적화에 주로 사용된다. 또한 모든 키가 인덱스가 되는 것은 아니며, 필요에 따라 인덱스를 생성하고 관리한다.

⇒ 따라서, index file의 구조 : **[search key][pointer]**

# Ordered Indices

ordered indices에서는 index entries들이 search key 값에 따라 정렬되어 저장된다.

### 1. clustering index (= primary index)

- table space에서 row들이 물리적으로 어떻게 정렬될 지 (clustered) 결정하는 index
- 즉, sequentially ordered file에서 정렬의 기준이 되는 index이다.
- 테이블 당 한 개만 존재 가능
- 보통 primary key가 clustering index이지만, 반드시 그렇지는 않다.

책으로 비유하면, **페이지를 알고 있어서 바로 해당 페이지를 펼치는 것과 같다.**

### 2. non-clustering index (= secondary index)

- index의 search key의 순서가 정렬되지 않은 index
- 검색 속도는 느리지만, 데이터의 입력/수정/삭제는 더 빠르다.
- 테이블 당 여러 개 존재 가능

책으로 비유하면, **목차에서 찾고자 하는 내용의 페이지를 찾고 나서 해당 페이지로 이동하는 것과 같다.**

### Clustering Index VS Non-Clustering Index

1. **Clustering Index**: 클러스터링 인덱스는 **데이터베이스 테이블의 물리적인 정렬 방식을 결정**한다. **테이블의 행은 클러스터링 인덱스를 기반으로 정렬되고,** 테이블 당 하나만 생성할 수 있으며, 테이블의 행 자체를 재정렬한다.
2. **Non-Clustering Index**: 비클러스터링 인덱스(또는 보조 인덱스라고도 함)는 **테이블의 물리적인 정렬에 영향을 미치지 않는다**. 대신 이 인덱스는 인덱스 키에 따라 **별도의 공간에 정렬된 테이블의 포인터 또는 참조를 유지**한다. 비클러스터링 인덱스는 테이블 당 여러 개를 가질 수 있다. 비클러스터링 인덱스를 사용하면 특정 키 값을 기반으로 데이터를 빠르게 찾을 수 있지만, 범위 쿼리나 정렬된 데이터를 검색하는 데는 클러스터링 인덱스보다 비효율적일 수 있다.

**요약하자면, 클러스터링 인덱스는 테이블의 물리적 정렬을 결정하며 테이블 당 하나만 생성할 수 있으나, 비클러스터링 인덱스는 테이블의 물리적 정렬에는 영향을 주지 않으며 테이블 당 여러 개를 생성할 수 있다.**

## Dense Index Files

이 경우, index file에 없으면 data file에도 없다.

- Dense index : Index record가 모든 search-key 값에 대해서 나타나는 경우
![image](https://blog.kakaocdn.net/dn/pr9jO/btrN5E98bHU/UsXkI1bGmhcMXRTCqbPSRK/img.png)

그림 상 왼쪽이 ‘Index file’, 오른쪽이 ‘data file’이다.

위에서 설명하였듯이 index filed의 구조는 search key와 pointer로 이뤄진다.

- 꼭 index file과 data file의 search key가 1:1로 존재하지는 않는다.

![image](https://blog.kakaocdn.net/dn/bSrZ0v/btrOceWV3gJ/7KGRuRBuSNklKs5twcQFH1/img.png)

이 경우 학과 이름이 search key인 경우일 것이다.

## Sparse Index Files

이 경우 dense index와 달리 index file은 일부의 search key만이 존재하여 index file에 없더라도 data file에서 등장할 수 있습니다.

- **Sparse index** : Index record가 일부 search-key 값에 대해서만 나타나는 경우

![image](https://blog.kakaocdn.net/dn/bcV26L/btrOgSS3nFz/6o1uy0bbGZuozLVBm7yLe1/img.png)

## Dense vs Sparse

1. **Dense Index**: Dense Index는 **테이블의 모든 행에 대해 인덱스 항목**을 가진다. 즉, 테이블의 각 행은 인덱스에 대응하는 항목을 가지므로 인덱스는 "밀도가 높다(dense)"고 말한다. 이러한 특성 때문에 Dense Index는 **특정 행에 대한 직접 접근을 빠르게 하지만, 인덱스 자체의 크기가 크므로 관리 비용이 높을 수 있다.**
2. **Sparse Index**: Sparse Index는 **테이블의 일부 행에 대해서만 인덱스 항목**을 가진다. 일반적으로 Sparse Index는 블록 또는 데이터 페이지의 첫 번째 레코드에 대한 항목만을 가진다. 이런 방식은 인덱스의 크기를 크게 줄여 **메모리를 효율적으로 사용**할 수 있게 하지만, Dense Index에 비해 특정 레코드를 찾는 데 더 **많은 시간이 소요**될 수 있다.

 Dense Index는 빠른 접근을 제공하지만 더 많은 저장 공간을 사용하며, Sparse Index는 저장 공간을 절약하지만 접근 시간이 약간 느릴 수 있다.

## Secondary Indices ⇒ 무조건 dense index

![image](https://blog.kakaocdn.net/dn/cAePQp/btrN78QqERp/jOcOyg1YvD8FmcRAWLVXak/img.png)

- **bucket** : Index file은 bucket의 주소를 가리키고, bucket에는 record의 주소가 들어있다.
- secendary index는 무조건 dense index이다.
- Non-clustering과 같은 의미이다.
    - 즉, 데이터의 물리적인 정렬에 영향을 미치지 않지만, 빠른 검색을 위한 참조를 제공

Secondary Index는 다음과 같은 경우에 유용하다:

1. **자주 조회되는 칼럼**: 특정 칼럼이 자주 조회되는 경우, 해당 칼럼에 대해 Secondary Index를 생성하면 검색 성능을 향상시킬 수 있다.
2. **복잡한 쿼리의 성능 향상**: 여러 테이블을 JOIN하는 복잡한 쿼리의 성능을 향상시키는 데에도 Secondary Index가 유용하다. 해당 칼럼에 대한 Index가 있으면, 데이터베이스는 해당 칼럼의 값을 빠르게 찾을 수 있다.

## Multilevel Index

만약 index file이 너무 커서 memory에 안 올라간다면, layer를 나눠서 관리해야 한다.

- outer index : sparse index
- inner index : basic index file
- 만약 outer index마저도 크다면, layer를 또 나눈다.

### Good tradeoff

- **For clustering index : block 단위의 sparse index**

일단 block에 접근하면 memory내에서 scan하여 빠르다. 따라서 dense 보다는 sparse index가 훨씬 더 유리하다.

- **For non-clustering index : dense index의 top을 가리키는 sparse index (multi-level index)**

![image](https://blog.kakaocdn.net/dn/oRfWO/btrN6mnQDxA/LnPlPwnJSKoqIYJqDTRi5K/img.png)

# B+Tree Index

indexed-sequentail file의 경우 file이 커지면서 성능이 하락하고 주기적으로 전체 파일에 대한 재정비가 필요하다.

그래서 B+tree 자료구조를 이용하여 index를 관리함으로써 이를 해결한다.

### B+Tree index의 장점, 단점

- 자동으로 삽입, 삭제에 대해서 재정비가 이뤄진다. (장)
- 전체 file에 대한 재정비가 필요하지 않다. (장)
- space overhead와 삽입, 삭제에 대한 overhead (단)

→ 단점에도 불구하고 얻을 수 있는 이점이 훨씬 더 많아서 보편적으로 사용됨

![image](https://blog.kakaocdn.net/dn/dqPvzQ/btrOfbFm70i/9m6K71SXvrVe2L1VOcj1dK/img.png)

## B+Tree 특징

- 엄밀히 얘기하면, **Binary tree, valance tree가 아니다!!**
- root부터 모든 leaf까지의 **path 길이가 같다**
- 자식 수
1. internal node의 자식 수 : **[n/2] ~ n         n=4→ 2~4**
    
    2. leaf node의 자식 수 : **[(n-1)/2] ~ n-1        n=4→ 1~3**
    
    3. root node의 자식 수 : (1) leaf 아닐 때 : **최소 2개,**  (2) leaf일 때 : **0~n-1개**
    
- 각 node들은 “logically”하게는 가깝지만 “phsically”하게는 그렇지 않다.
- **non-leaf level에서는 sparse indices**이다.
- 상대적으로 level의 개수가 크지 않아서 성능이 좋다 
1. root 밑 level은 최소 2*[n/2]개의 값, 다음 level은 최소 2* [n/2] * [n/2]
    
    2. K개의 search key가 있다면 tree height : 최대 log[n/2] (K)
    

## B+Tree Node Structure

![image](https://blog.kakaocdn.net/dn/ddPw8n/btrOgxuGr31/bV8iQD19MTbvAEQJGjvqBk/img.png)

- K : search key 값
- P : pointer (자식 노드, record, bucket)
- **node 내 search key는 정렬**됨 : K1 < K2 < K3 < …. < Kn-1

### Leaf Nodes in B+Trees

Leaf node의 특징

- P 는 file내 record 중 searck key값이 K인 record를 가리킨다.
- leaf node L에 대해서 i< j 일 때, Li의 search-key value는 Lj의 search-key보다 작거나 같다.
- 마지막 Pointer는 다음 leaf node를 가리킨다.

### Non-Leaf Nodes in B+Trees

- **multi-level sparse index**를 생성한다.
- tree 내 search key값이 정렬되어 있다.
1. P1이 가리키는 sub tree에 있는 모든 search key 값들이 K1보다 작다. (구조 참고)
2. 2≤i≤n-1일 때, Pi이 가리키는 sub tree에 있는 모든 search key들은 Ki-1보다 크고, Ki보다 작다.
3. Pn이 가리키는 sub tree에 있는 모든 search key 값들은 Kn-1보다 크다.

## Queries on B+Trees

- K개의 search key value → tree height : 최대 log[n/2] (K)
- 따라서, K = 1,000,000 이고 n =100 이면 tree height는 log[50](1,000,000) = 4정도 된다.
- 즉, 4번만 거치면 원하는 값을 찾을 수 있다.
- disk에서는 차이가 많이 나지만, ssd에서는 큰 차이가 없다.

### Range Queries

- 주어진 range내 serach key value가 속하는 모든 record를 찾는 query
- 이 경우 clustering index라면 data file에서의 scan이 쉽겠지만, non-clustering index라면 data file로 접근해서 읽을 때 magenetic disk의 비용이 훨씬 많이 들게 된다.

![image](https://blog.kakaocdn.net/dn/cmLxpN/btrOgRGDVZx/rPtZpYpIVyPR1MxLsTU1E1/img.png)

  

# B+ Tree Extensions

## B+Tree File Organization

> p.651
> 
> 
> We solve the degradation problem for **storing the actual records** by using the leaf level
> of the B+-tree to organize the blocks containing the actual records. We use the B+-tree
> structure **not only as an index, but also as an organizer for records in a file.**
> 
- 여기서는 Leaf node 가 pointer 대신 record를 저장한다.
- 삽입, 수정, 삭제가 이뤄지더라도 data들이 clustered되도록 도와준다.
- record는 pointer보다 용량이 크므로, leaf node에 저장될 수 있는 record의 최대 개수는 nonleaf node에서의 pointer 개수보다 작다.

![image](https://blog.kakaocdn.net/dn/mlvFw/btrOgyf71Au/WvoM3njUphr4k6dBTs8qIk/img.png)

- space utilization이 필요하다. (pointer 대신 record를 저장하므로)
- 이를 위해서 split과 merge 과정에서 sibling node들을 골고루 퍼트린다. (7,7,10 vs 8,8,8)

## B Tree Index Files

B+ Tree에서는 internode에 있는 search key가 반드시 leaf node에 나타나게 된다.
따라서 조회를 위해서는 무조건 leaf까지 가야한다.

반면, B Tree에서는 search-key가 오직 한 번만 나타난다.

- search key가 nonleaf node에서도 나타난다.
- leaf까지 갈 필요 없이 바로 찾을 수도 있다.
- 구조

![image](https://blog.kakaocdn.net/dn/1iWLh/btrOdh0crF7/yCucsoxDtqZV1apCY1TIrK/img.png)

- Bi : bucket or file record pointer

> **fan-ou**t: number of pointers to child nodes in a node.
**fan-out이 클수록 tree의 height가 작다**
> 

### B Tree 장단점

장점

1. B+ Tree에 비해서 적은 node로 구성할 수도 있다.
2. leaf 까지 가기 전에 찾을 수도 있다.

단점

1. 대부분은 leaf까지 가야됨
2. depth가 깊다(height가 높다) : fan-out이 작다.
3. 삽입과 삭제가 더 복잡하다.
4. 구현이 어렵다

따라서 대부분 B+ Tree를 사용한다.

![image](https://blog.kakaocdn.net/dn/dckTMr/btrOcfhi1au/cAGx0KAmunQUoKztzgoIc0/img.png)

# Hash Indices

## Static Hashing

- bucket : entries들을 저장하는 storage unit
- hash function을 이용한 search-key값을 통해 entry의 bucket을 얻는다.
- hash function, h가 search-key set K를 bucket address set B로 변환시킨다.
- In a hash index → bucket이 pointer를 저장
- In a hash file-organization → bucket이 record를 저장

## Handling of Bucket Overflows

hash 함수를 아무리 잘 만들었더라도 Bucket overflow가 발생할 수 있다.

### bucket overflow 원인

- 충분치 않은 bucket양
- hash 함수가 non-uniform하기 분배한 경우
- multiple record가 같은 search-key값을 가진 경우

### overflow chaining (closed addressing, closed hashing)

→ linked list로 해결

![image](https://blog.kakaocdn.net/dn/GjcFn/btrOfazNQTH/hUoSqW1VXer6oPpldUkytk/img.png)

### Example of Hash Index

![image](https://blog.kakaocdn.net/dn/cvsPBu/btrOc74swAV/8xPtR1xCvrUpggQWAZPjA1/img.png)

### Deficiencies of Static Hashing

DB는 시간이 지남에 따라 grow하거나 shrink하는데, static hash index이기 때문에 db가 커지면 성능이 안 좋아지고, 작아지면 공간이 낭비된다.

이에 대한 해결책은,

- **periodic re-organization** with a **new hash function → cost가 비싸다**
- **Dynamic Hashing** (better soultion)

## Ordered Indexing vs Hashing

- 주기적으로 B+ tree를 다시 만든다.
- access time의 경우 B+tree는 무조건 leaf까지 가야하고, hash는 경우에 따라 다르다.
- Hashing ⇒ 특정 값을 찾는 쿼리에 적합하다.
- B+ Tree ⇒ range 쿼리에 적합하다.
