# Project Description

**Deployed Frontend URL:** <your Vercel/Netlify link here>  

**Solana Program ID:** `8E5L54gG4Hi8MVDoacSJDmSCksuH62TpyikaVaBRMCqw`  

---

## Project Overview

### Description
This project is a decentralized **tipping dApp** built on Solana using Anchor.  
It allows users to send tips (in SOL) to other wallets while tracking the total amount tipped across all users.  
The program demonstrates the use of **Program Derived Addresses (PDAs)**, account initialization, lamport transfers, and state persistence.

### Key Features
- **Initialize Tipping Account** – Create the global tipping account via a PDA.  
- **Send Tips** – Transfer SOL from the sender to a recipient while updating the total tips counter.  
- **Track Stats** – Keep an on-chain record of the cumulative SOL tipped through the dApp.  

### How to Use the dApp
1. **Connect Wallet** – Connect your Solana wallet (e.g., Phantom).  
2. **Initialize Tipping Account** – If no tipping account exists, initialize it.  
3. **Send a Tip** – Enter a recipient’s wallet address and specify the amount of SOL to send.  
4. **View Success Notification** – The dApp displays a confirmation and updates the running total of tips.  

---

## Program Architecture

The program is built around **one PDA** and **two main instructions** (`initialize` and `send_tip`).  

### PDA Usage
- **Tipping PDA** – Derived from the static seed `["tipping"]`, ensuring a single global tipping account for the program.  

### Program Instructions
- **Initialize** – Creates the tipping account PDA and sets the total tips to `0`.  
- **Send Tip** – Transfers SOL from sender to recipient and updates the tipping account’s total tips.  

### Account Structure
```rust
#[account]
pub struct TippingAccount {
    pub total_tips: u64,  // Total lamports tipped across the dApp
}


## Testing

### Test Coverage
Comprehensive test suite covering all instructions with both successful operations and error conditions to ensure program security and reliability.

**Happy Path Tests:**
- **Initialize Counter**: Successfully creates a new counter account with correct initial values  
- **Increment Counter**: Properly increases count and total_increments by 1  
- **Reset Counter**: Sets count to 0 while preserving owner and total_increments  

**Unhappy Path Tests:**
- **Initialize Duplicate**: Fails when trying to initialize a counter that already exists  
- **Increment Unauthorized**: Fails when non-owner tries to increment someone else's counter  
- **Reset Unauthorized**: Fails when non-owner tries to reset someone else's counter  
- **Account Not Found**: Fails when trying to operate on non-existent counter  

### Running Tests
```bash
yarn install    # install dependencies
anchor test     # run tests


### Additional Notes for Evaluators

This tipping dApp was my first full Solana project combining **Anchor (Rust)** and a **React/TypeScript frontend**.  

The main challenges were:  
- Correctly setting up and fetching the PDA  
- Handling SOL transfers with `system_instruction::transfer`  
- Debugging frontend transaction confirmation in Phantom wallet  

Through this project, I learned how to properly:  
- Use PDAs effectively  
- Pass accounts between the frontend and program  
- Confirm transactions on Devnet  
