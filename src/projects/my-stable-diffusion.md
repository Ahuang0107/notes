# My-Stable-Diffusion

尝试基于Stable Diffusion训练一个能生成2d像素游戏资产的模型

首先是先尝试在本地把Stable Diffusion跑起来

```
× Encountered error while trying to install package.
╰─> grpcio
```
https://github.com/grpc/grpc/issues/30064
跑`pip install -r requirements.txt`时加上`GRPC_PYTHON_BUILD_SYSTEM_OPENSSL=true GRPC_PYTHON_BUILD_SYSTEM_ZLIB=true`，
`GRPC_PYTHON_BUILD_SYSTEM_OPENSSL=true GRPC_PYTHON_BUILD_SYSTEM_ZLIB=true pip install -r requirements.txt`

## Reference

[Run Stable Diffusion on M1](https://replicate.com/blog/run-stable-diffusion-on-m1-mac)

[Error occurred at "pip install grpcio" on Mac M1](https://github.com/grpc/grpc/issues/30064)