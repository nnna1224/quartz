[[python]]においてファイルパスを記述する際に，同じようなパスが重複してしまうことがあった．
コードを美しくするために，処理をある程度まとめた．
>[!TIP] 意図が伝わりやすく，見やすいコードを[[Pythonicなコードというらしい．

```python
SCRIPT_DIR = os.path.dirname(os.path.abspath(__file__))

resource_names = ["j2a_src", "j2a_ref", "a2j_src", "a2j_ref"]
resource_files = [f"../../resources/test_{name}.txt" for name in resource_names]

def path_to_list(path: str) -> List[str]:
    with open(path, mode='r', encoding='utf-8') as f:
        return [line.strip() for line in f if line.strip() != ""]

data_list = [path_to_list(os.path.join(SCRIPT_DIR, path)) for path in resource_files]

j2a_src, j2a_ref, a2j_src, a2j_ref = data_list
```

もっと良い方法があるかもしれない．