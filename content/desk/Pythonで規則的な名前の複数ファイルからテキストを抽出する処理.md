[[python]]においてファイルパスを記述する際に，同じようなパスが重複してしまうことがあった．
コードを美しくするために，処理をある程度まとめた．

```python
resource_names = ["j2a_src", "j2a_ref", "a2j_src", "a2j_ref"]
resource_files = [f"../../resources/test_{name}.txt" for name in resource_names]

def path_to_list(path: str) -> List[str]:
    with open(path, mode='r', encoding='utf-8') as f:
        return [line.strip() for line in f if line.strip() != ""]

script_dir = os.path.dirname(os.path.abspath(__file__))
data_list = [path_to_list(os.path.join(script_dir, path)) for path in resource_files]

j2a_src, j2a_ref, a2j_src, a2j_ref = data_list
```

もっと良い方法があるかもしれない．