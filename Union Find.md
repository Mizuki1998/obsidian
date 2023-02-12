###  Union Find とは何か?

  Union Find は [[Graph Algorithm]] の1種でグループ分けを効率的に管理することができるデータ構造です 

具体的には以下の2種類のクエリを高速に処理することができます

1. 回答クエリ：要素uと要素vが同じグループにあるかを答える
2. 統合クエリ：要素uを含むグループと要素vを含むグループを統合する

### 回答クエリの処理

頂点vの根をroot(x)と表す時、要素uと要素vが同じグループかどうかは次のように判定することができます

> root(u) = root(v)の場合：同一のグループ
> root(u) != root(v)の場合：異なるグループ

### 統合クエリの処理

「二つのグループの根を繋ぐ」という方法で処理することができます。
頂点xの親をpar[x]とするとき、「頂点uを含むグループ」と「頂点vを含むグループ」は次の処理によって統合することができます。

> par[root(u)] = root(v) とする

### Union Find の計算量

Union Findは頂点xの根を求める関数root(x)が基本となっています。これは下記のように実装でき、計算回数は（頂点xから根までの距離)に比例します。

```python:Union Find
int root(int x) {
	while(true) {
		if(par[x] == -1) {
			break; // 1個先(親)がいなければ、ここが根
		}
		x = par[x];
	}
	return x;			 
}
```

しかしこれだけだと、計算量がO(N)となり、問題によっては実行制限に間に合わない場合があります。そこで改良版のUnion Findを用います。
それは、<strong> 頂点数の多いグループを上に持っていく</strong> という工夫です。これだけで計算量がO(N)からO(log N)mで削減されます。この手法は[[Union by Size]]と呼ばれています。

### 参考
- 競技プログラミングの鉄則 P374
- [Git Hub](https://github.com/E869120/kyopro-tessoku/blob/main/codes/java/chap09/answer_A66.java) 









