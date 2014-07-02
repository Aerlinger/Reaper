# Reaper

A domain specific language for managing jobs across multiple processes

# Usage



```
type Worker
  available::Boolean
  rref::RemoteRef
  pid::Int
end
```

workers::Array{Worker} = []

function setup_workers()
  workers = []

  for i=1:workers()
    push!(workers, worker(true, i)
  end
end

function available_workers
  filter(workers) do worker
    worker.available
  end
end

function get_available_worker()
  first(available_workers())
end

function find_worker_by_pid(pid::Int)
    filter(workers) do worker
      worker.pid == pid
    end
end

function unavailable(f::Function)
  f()
end

function fork(f::Function, args)
  worker = get_available_worker()
  rref = remotecall(worker.pid, f, args)

end

```
before_fork do result
end
```

```
after_fork do result
end
```

```
if_full do
end
```

```
spawn_with_timeout(15) do

end
```

Reactor

```
for proc in procs()
  if isready
end
```

# Configuration

num_workers
timeout
