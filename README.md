forked for codellama with llama-cpp-python

## setup server
```bash
python3 -m venv .venv
. .venv/bin/activate

# enable Metal GPU on MacOS https://github.com/abetlen/llama-cpp-python/blob/main/docs/install/macos.md
CMAKE_ARGS="-DLLAMA_METAL=on" FORCE_CMAKE=1 pip install llama-cpp-python[server]

# download model https://huggingface.co/TheBloke/CodeLlama-7B-GGUF
python3 -m llama_cpp.server --model models_path/codellama-7b.Q4_K_M.gguf --n_gpu_layers 35
```

```lua
-- lazy config
  {
    'yanyaoer/cmp-fauxpilot',
    dependencies = 'hrsh7th/nvim-cmp',
    config = function()
      local fauxpilot = require('cmp_fauxpilot.config')
      fauxpilot:setup({
        host = 'http://127.0.0.1:8000',
        model = 'copilot-codex',
        endpoints = '/v1/engines/copilot-codex/completions',
        max_tokens = 500,
        max_lines = 1000,
        max_num_results = 4,
        temperature = 0.6,
      })
    end
  }
```

# cmp-fauxpilot

fauxpilot source for [hrsh7th/nvim-cmp](https://github.com/hrsh7th/nvim-cmp)

# Install

## Using a plugin manager

Using plug:

```viml
Plug 'nzlov/cmp-fauxpilot'
```

Using plug on windows:

```viml
Plug 'nzlov/cmp-fauxpilot'
```

Using [Lazy](https://github.com/folke/lazy.nvim/):

```lua
return require("lazy").setup({
 {
     'nzlov/cmp-fauxpilot',
     dependencies = 'hrsh7th/nvim-cmp',
 }})
```

Using [Packer](https://github.com/wbthomason/packer.nvim/):

```lua
return require("packer").startup(
	function(use)
		use "hrsh7th/nvim-cmp" --completion
		use {'nzlov/cmp-fauxpilot', requires = 'hrsh7th/nvim-cmp'}
	end
)
```

And later, enable the plugin:

```lua
require'cmp'.setup {
	sources = {
		{ name = 'cmp_fauxpilot' },
	},
}
```

# Setup

```lua
local fauxpilot = require('cmp_fauxpilot.config')

fauxpilot:setup({
    host = 'http://localhost:5000',
    model = 'py-model',
    max_tokens = 100,
    max_lines = 1000,
    max_num_results = 4,
    temperature = 0.6,
})
```

# More
Based on [tzachar/cmp-tabnine](https://github.com/tzachar/cmp-tabnine)
