# Measuring Harmfulness of Computer-Using Agents

<div align="center">

[🤗 [Hugging Face](https://huggingface.co/datasets/CUAHarm/CUAHarm)] [📄 [Paper](https://arxiv.org/abs/2508.00935)]
</div>

## 📋 Introduction

**CUAHarm** is a benchmark designed to evaluate the safety risks of Computer-Using Agents (CUAs) - AI agents that can autonomously control computers to perform multi-step actions.

### Key Features

**🔍 CUAHarm Dataset**: A collection of 104 realistic misuse scenarios, including 52 computer use tasks that require direct system interaction. These tasks cover seven categories of malicious objectives: credential theft, privilege escalation, network exploitation, system disruption, data tampering, forensic evasion, and tool utilization.

**💻 Direct Terminal Access**: CUAHarm supports computer-using agents with full system access through direct terminal interaction.

**💰 Token Cost Calculation**: Built-in functionality to track token usage during agent execution.


## 💾 Installation
### VMware/VirtualBox (Desktop, Laptop, Bare Metal Machine)
Suppose you are operating on a system that has not been virtualized (e.g. your desktop, laptop, bare metal machine), meaning you are not utilizing a virtualized environment like AWS, Azure, or k8s.

1. First, clone this repository and `cd` into it. Then, install the dependencies listed in `requirements.txt`. It is recommended that you use the latest version of Conda to manage the environment, but you can also choose to manually install the dependencies. Please ensure that the version of Python is >= 3.9.
```bash
# Clone the CUAHarm repository
git clone https://github.com/db-ol/CUAHarm

# Change directory into the cloned repository
cd CUAHarm

# Optional: Create a Conda environment for CUAHarm
# conda create -n cuaharm python=3.9
# conda activate cuaharm

# Install required dependencies
pip install -r requirements.txt
```

2. Install [VMware Workstation Pro](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html) (for systems with Apple Chips, you should install [VMware Fusion](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware+Fusion)) and configure the `vmrun` command.  The installation process can refer to [How to install VMware Worksation Pro](desktop_env/providers/vmware/INSTALL_VMWARE.md). Verify the successful installation by running the following:
```bash
vmrun -T ws list
```
If the installation along with the environment variable set is successful, you will see the message showing the current running virtual machines.
> **Note:** We also support using [VirtualBox](https://www.virtualbox.org/) if you have issues with VMware Pro. However, features such as parallelism and macOS on Apple chips might not be well-supported.

All set! Our setup script will automatically download the necessary virtual machines and configure the environment for you.


## 🧪 Experiments
If you wish to run an agent with direct terminal access used in our paper, for example, under the GPT-4o setting:

Set **OPENAI_API_KEY** environment variable with your API key
```bash
export OPENAI_API_KEY='changeme'
```

Assuming your VM path is `./vmware_vm_data/Ubuntu0/Ubuntu0.vmx`:

**Step 1**: Open a terminal in your VM and save a screenshot named `CUAHarm`.

**Step 2**: Run the evaluation command:

```bash
python run.py --path_to_vm ./vmware_vm_data/Ubuntu0/Ubuntu0.vmx --observation_type terminal --model gpt-4o-2024-11-20 --test_all_meta_path evaluation_examples/test_computer_use_tasks.json --result_dir ./results
```
The results, which include screenshots, actions, and video recordings of the agent's task completion, will be saved in the `./results` directory in this case.


## ❓ FAQ
### What is the username and password for the virtual machines?
The username and password for the virtual machines are as follows:
- **Ubuntu:** `user` / `password`

### How to setup the account and credentials for Google and Google Drive?

See [Account Guideline](ACCOUNT_GUIDELINE.md).

### How can I configure a proxy for the VM if I'm behind a GFW?

See [Proxy Guideline](PROXY_GUIDELINE.md).


## 📚 Citation

If you find this work useful, please consider citing our paper:

```bibtex
@misc{tian2025measuringharmfulnesscomputerusingagents,
      title={Measuring Harmfulness of Computer-Using Agents}, 
      author={Aaron Xuxiang Tian and Ruofan Zhang and Janet Tang and Jiaxin Wen},
      year={2025},
      eprint={2508.00935},
      archivePrefix={arXiv},
      primaryClass={cs.CR},
      url={https://arxiv.org/abs/2508.00935}, 
}
```


## ⚖️ License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

**Acknowledgments**: This codebase is based on the [OSWorld](https://github.com/xlang-ai/OSWorld) framework, which is also licensed under Apache License 2.0.
