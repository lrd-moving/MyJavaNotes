## HashMap

### 数据结构

1. K、V数组（buckets）

   ```Java
       /**
        * The table, initialized on first use, and resized as
        * necessary. When allocated, length is always a power of two.
        * (We also tolerate length zero in some operations to allow
        * bootstrapping mechanics that are currently not needed.)
        */
       transient Node<K,V>[] table;
   ```

   

2. LinkedHashMap or TreeMap， key相同的情况下 （同一个bucket下的数据结构）

### 关键属性

- 

  ```java
  //默认初始bucket大小
      static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16
      
  //最大容量
      static final int MAXIMUM_CAPACITY = 1 << 30;
  
  //默认加载因子
      static final float DEFAULT_LOAD_FACTOR = 0.75f;
    
  //bucket的树化阈值，bucket中容量大于此阈值，数据结构变为树
      static final int TREEIFY_THRESHOLD = 8;
  
  //bucket的非树化阈值，bucket中容量小于此阈值，数据结构变链表
      static final int UNTREEIFY_THRESHOLD = 6;
  
  //树化容量阈值，capacity()小于此值时，不进行树化
      static final int MIN_TREEIFY_CAPACITY = 64;
  ```

### 关键方法

- **put：** 主要分为三步，可参考 （[](https://www.cnblogs.com/zhaojj/p/7805376.html)）

  1. 实例化buckets数组（如果未实例化）；
  2. 计算hash值和bucket位置索引，实例化bucket（如果未实例化）；
  3. 添加到bucket中，如果key相同，进行替换，返回原先的value值；

  ```Java
      /**
       * Implements Map.put and related methods
       *
       * @param hash hash for key
       * @param key the key
       * @param value the value to put
       * @param onlyIfAbsent if true, don't change existing value
       * @param evict if false, the table is in creation mode.
       * @return previous value, or null if none
       */
      final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                     boolean evict) {
          Node<K,V>[] tab; Node<K,V> p; int n, i;
          //判断table是否已初始化
          if ((tab = table) == null || (n = tab.length) == 0)
              n = (tab = resize()).length;
          
          // 使用 i = (n - 1) & hash 取hash的低X位作为bucket的位置索引。buckets数量必为2的倍数。
          if ((p = tab[i = (n - 1) & hash]) == null)
              tab[i] = newNode(hash, key, value, null);
          else {
              Node<K,V> e; K k;
              
              // 若key冲突，则进行替换
              if (p.hash == hash &&
                  ((k = p.key) == key || (key != null && key.equals(k))))
                  e = p;
              //key不冲突，树结构添加
              else if (p instanceof TreeNode)
                  e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
              //key不冲突，丽娜表结构添加
              else {
                  for (int binCount = 0; ; ++binCount) {
                      // 挂链
                      if ((e = p.next) == null) {
                          p.next = newNode(hash, key, value, null);
                          if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                              treeifyBin(tab, hash);
                          break;
                      }
                      
                      //链表中有key冲突，进行替换
                      if (e.hash == hash &&
                          ((k = e.key) == key || (key != null && key.equals(k))))
                          break;
                      p = e;
                  }
              }
              if (e != null) { // existing mapping for key
                  V oldValue = e.value;
                  if (!onlyIfAbsent || oldValue == null)
                      e.value = value;
                  afterNodeAccess(e);
                  return oldValue;
              }
          }
          ++modCount;
          if (++size > threshold)
              resize();
          afterNodeInsertion(evict);
          return null;
      }
  ```

  

- **get：**  get相对比较简单

  ```Java
      /**
       * Implements Map.get and related methods
       *
       * @param hash hash for key
       * @param key the key
       * @return the node, or null if none
       */
      final Node<K,V> getNode(int hash, Object key) {
          Node<K,V>[] tab; Node<K,V> first, e; int n; K k;
          
          //找到bucket
          if ((tab = table) != null && (n = tab.length) > 0 &&
              (first = tab[(n - 1) & hash]) != null) {
              //校验第一个元素
              if (first.hash == hash && // always check first node
                  ((k = first.key) == key || (key != null && key.equals(k))))
                  return first;
              //遍历树or链表找到node
              if ((e = first.next) != null) {
                  if (first instanceof TreeNode)
                      return ((TreeNode<K,V>)first).getTreeNode(hash, key);
                  do {
                      if (e.hash == hash &&
                          ((k = e.key) == key || (key != null && key.equals(k))))
                          return e;
                  } while ((e = e.next) != null);
              }
          }
          return null;
      }
  ```

### keySet  、  entrySet、 values

- 这三个Set均为当前HashMap的视图，并不存储实际的数据，通过直接和 HashMap 的 iterator 挂钩来反应HashMap的变化。 [](https://www.cnblogs.com/dsj2016/p/5551059.html)

