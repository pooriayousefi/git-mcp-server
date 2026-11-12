# git-mcp-server

A standalone C++20 Model Context Protocol (MCP) server for Git repository inspection and operations.

## Tools

git_init, git_status, git_diff, git_log, git_show, git_add, git_commit, git_branch, git_current_branch, git_checkout, git_create_branch, git_reset, git_stash, git_remote, git_fetch, git_pull, git_push, git_clone

## Dependencies

The MCP protocol, server, transport, process, JSON, and HTTP implementations are provided by [`pooriayousefi/mcpxx`](https://github.com/pooriayousefi/mcpxx), included as a pinned Git submodule at `external/mcpxx` (commit `0ec0e6ac04acc46fb7c6160f1a16a2ead19ee4a0`).

## Requirements

- C++20 compiler (Clang or GCC)
- POSIX threads
- Git with submodule support

## Clone and build

```sh
git clone --recurse-submodules https://github.com/pooriayousefi/git-mcp-server.git
cd git-mcp-server
make
```

If already cloned without submodules, run `git submodule update --init --recursive` first.

To compile directly:

```sh
mkdir -p bin
clang++ -std=c++20 -O2 -pthread -I external/mcpxx/include \\
  src/git_mcp_tool_server.cpp -o bin/git_mcp_tool_server
```

On Windows with MinGW, add `-lws2_32`.

## Run

The default transport is stdio:

```sh
./bin/git_mcp_tool_server
```

For Streamable HTTP:

```sh
./bin/git_mcp_tool_server http 127.0.0.1 8099
```

The HTTP endpoint is `/mcp`. Bind to loopback unless suitable network controls are configured; HTTP transport is not an authentication boundary.

## License

Apache-2.0. See [LICENSE](LICENSE).
