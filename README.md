# @reverse-craft/smart-fs-mcp

MCP (Model Context Protocol) server that exposes smart-fs functionality as AI-accessible tools. Enables AI assistants to read, search, and analyze code with source map support.

## Features

- **read_code_smart** - Read and beautify code files with source map coordinates
- **search_code_smart** - Search in beautified code, returns original positions
- **find_usage_smart** - Find variable/function definitions and references
- **apply_custom_transform** - Apply Babel plugins for code transformation

## Installation

```bash
npm install @reverse-craft/smart-fs-mcp
```

## Usage

### As MCP Server

Add to your MCP configuration (e.g., Claude Desktop, Kiro):

```json
{
  "mcpServers": {
    "smart-fs": {
      "command": "npx",
      "args": ["@reverse-craft/smart-fs-mcp"]
    }
  }
}
```

### Run Directly

```bash
npx @reverse-craft/smart-fs-mcp
```

## MCP Tools

### read_code_smart

Read and beautify code with optional line range and truncation.

```typescript
{
  filePath: string;      // Path to file
  startLine?: number;    // Start line (1-based)
  endLine?: number;      // End line (1-based)
  charLimit?: number;    // String truncation length (default: 300)
  maxLineChars?: number; // Max chars per line (default: 500)
}
```

### search_code_smart

Search in beautified code with context lines.

```typescript
{
  filePath: string;       // Path to file
  query: string;          // Search query
  isRegex?: boolean;      // Use regex matching
  caseSensitive?: boolean;
  contextLines?: number;  // Lines of context (default: 2)
  maxMatches?: number;    // Max results (default: 50)
}
```

### find_usage_smart

Find all definitions and references of an identifier.

```typescript
{
  filePath: string;       // Path to file
  identifier: string;     // Variable/function name
  targetLine?: number;    // Target line for precise binding
  maxReferences?: number; // Max references (default: 10)
}
```

### apply_custom_transform

Apply Babel plugin transformations.

```typescript
{
  filePath: string;       // Path to file
  pluginPath: string;     // Path to Babel plugin
  outputPath?: string;    // Output file path
}
```

## Output Format

All tools return formatted output with source map coordinates:

```
/path/to/file.js (1-20/5000)
Src=original position for breakpoints
    1 L1:0       var _0x1234 = function() {
    2 L1:25        var data = "SGVsbG8=...[TRUNCATED]...";
    3 L1:50078    return decode(data);
```

## Related Packages

- **[@reverse-craft/smart-fs](https://github.com/reverse-craft/smart-fs)** - Core library
- **[@reverse-craft/ai-tools](https://github.com/reverse-craft/ai-tools)** - AI-powered analysis tools

## License

MIT
