# FastAi Course 22 Part 2

## Learnings

1. Pytorch overrides __setattr__(k,v) for registering layers inside a module and adds them to a dictionary, therefore the method parameters() knows how to loop over all weights and biases.
1. Within the forward method, we can use the reduce approch to iterate over all layers:
   ```def forward(self, x): return reduce(lambda val, layer: layer(val), self.layers, x) ``` instead of 
   ```
    def forward(self, x):
        for l in self.layers: x = l(x)
        return x
    ```
1. nn.Sequential does all of that for us: ```model = nn.Sequential(nn.Linear(n,nh), nn.ReLU(), nn.Linear(nh,10))```
1. The optim module lets us do opt.step() which updates all the parameters and opt.zero_grad() for zeroing the gradients.
1. A Dataset combines the x and y
    ```
    class Dataset():
        def __init__(self, x, y): self.x, self.y = x,y
        def __len__(self): return len(self.x)
        def __getitem__(self, i): return self.x[i], self.y[i]
    ```
1. A DataLoader automatically slices the correct batch out of the Dataset:
    ```
    class DataLoader():
        def __init__(self, ds, bs): self.ds, self.bs = ds, bs
        def __iter__(self):
            for i in range(0, len(self.ds), self.bs): yield self.ds[i:i+self.bs]
    ```
1. Random sampling: training set should be in random order, but validation set not.
    ```
    class Sampler():
        def __init__(self, ds, shuffle=False): self.n, self.shuffle = len(ds), shuffle
        def __iter__(self):
            res = list(range(self.n))
            if self.shuffle: random.shuffle(res)
            return iter(res)

    class BatchSampler():
        def __init__(self, sampler, bs, drop_last=False): self.sampler, self.bs, self.drop_last = sampler, bs, drop_last
        def __iter__(self): yield from fc.chunked(iter(self.sampler), self.bs, drop_last=self.drop_last)

    def collate(b):
        xs, ys = zip(*b)
        return torch.stack(xs), torch.stack(ys)

    def DataLoader():
        def __init__(self, ds, batchs, collate_fn=collate): ...
        def __iter__(self): yield from (self.collate_fn(self.ds[i] for i in b) for b in self.batchs)

    train_samp = BatchSampler(Samplel(train_ds, shuffle=True), bs)
    train_dl = DataLoader(train_ds, batchs=train_samp)
    xb, yb = next(iter(valid_dl))
    ```
1. The collate function is preparing the data for the model and doing preprocessing like resampling images ans so on.
1. Typically, the DataLoader is implemented with parallel processing in order to distribute the data loading.
1. All of the above implemented Samplers are provided in pytorch with a ```SequentialSampler``` and a ```RandomSampler```
1. *args and **kwargs: allows you to pass an unspecified nuber of arguments to a function. *args is a non-keyworded variable length list, **kwargs is a variable length dict.
1. ```*``` can also be used to unpack a list:
    ```
    def my_sum(a, b, c): print(a + b + c)
    my_list = [1, 2, 3]
    my_sum(*my_list)
    ```