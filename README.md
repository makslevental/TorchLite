# TorchLite

Very early days of compiling PyTorch independently of `aten`...

```python
from nn.conv import Conv2d
from nn.module import Module


class DemoConv(Module):
    def __init__(self):
        super().__init__()

        self.conv = Conv2d(1, 2, 3)

    def forward(self, x):
        return self.conv(x)
```

```shell
$ python compiler.py

>>> CallExpr:7(
>>>   SuperExpr:7(
>>>     __init__
>>>     CallExpr:7(
>>>       NameExpr(super)
>>>       Args()))
>>>   Args()) None
>>> SuperExpr:7(
>>>   __init__
>>>   CallExpr:7(
>>>     NameExpr(super)
>>>     Args())) def ()
>>> CallExpr:9(
>>>   NameExpr(Conv2d [nn.conv.Conv2d])
>>>   Args(
>>>     IntExpr(1)
>>>     IntExpr(2)
>>>     IntExpr(3))) nn.conv.Conv2d
>>> IntExpr(1) Literal[1]?
>>> IntExpr(2) Literal[2]?
>>> IntExpr(3) Literal[3]?
>>> NameExpr(Conv2d [nn.conv.Conv2d]) def (in_channels: builtins.int, out_channels: builtins.int, kernel_size: Union[builtins.int, Tuple[builtins.int, builtins.int]], stride: Union[builtins.int, Tuple[builtins.int, builtins.int]] =, padding: Union[builtins.str, Union[builtins.int, Tuple[builtins.int, builtins.int]]] =, dilation: Union[builtins.int, Tuple[builtins.int, builtins.int]] =, groups: builtins.int =, bias: builtins.bool =, padding_mode: builtins.str =, device: Any =, dtype: Any =) -> nn.conv.Conv2d
>>> MemberExpr:9(
>>>   NameExpr(self [l])
>>>   conv*) nn.conv.Conv2d
>>> NameExpr(self [l]) demo.DemoConv
>>> MemberExpr:12(
>>>   NameExpr(self [l])
>>>   conv) nn.conv.Conv2d
>>> NameExpr(self [l]) demo.DemoConv
```
