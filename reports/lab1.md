[toc]

# 1. lab1 实现说明

实现参考[chapter3(lab1)实践的框架和代码分析讲解](https://cloud.tsinghua.edu.cn/f/17a7c9d9b57f4838ae5f/)

```rust
fn sys_trace(_trace_request: usize, _id: usize, _data: usize) -> isize
```

**功能一： 返回 id 地址处的值**

> ```rust
> let addr = _id as *const u8;
> unsafe { *addr as isize }
> ```

**功能二： 在 id 地址处写入 data 并返回 0**

> ```rust
> let addr = _id as *mut u8;
> unsafe { *addr = _data as u8; }
> 0
> ```
>
> 

**功能三： 统计系统调用次数**

> 1. 首先需要在 //task.rs 内 TaskControlBlock 结构体 内添加 `pub syscall_times: [u32; MAX_SYSCALL_NUM],`成员，记录调用系统接口次数
> 2. 在 //task/mod.rs 内 TaskManager 实现并添加 两个对外接口函数 add_syscall_times(), get_syscall_times() 
> 3. 在 //src/syscall/mod.rs 内 syscall() 入口函数添加 add_syscall_times() 即可实现每次系统调用时统计次数

# 2. 简答题

## 1. ch2b_bad_*.rs

```bash
// ch2b_bad_address
[kernel] PageFault in application, bad addr = 0x0, bad instruction = 0x804003a4, kernel killed it.
```

