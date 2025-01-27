Bitcoin blocks are composed of transactions, and every transaction in a block can only depend on transactions that are [earlier than it in the block or were in a previous block](https://github.com/bitcoinbook/bitcoinbook/blob/develop/ch12_mining.adoc).

Sometimes big chunks of transactions come through which all depend on each other. These could be spam, they could also be someone [embedding a message in the blockchain](https://mempool.space/block/0000000000000000000341cc26cda4af82cd25f7063c448772228cbf2836915b?audit=false).

Block packing is the same as [Bin packing](https://en.wikipedia.org/wiki/Bin_packing_problem?useskin=vector), which is NP-hard.

During an exercise at Chaincode Labs, we had to pack optimal blocks.

Some things that helped me out:

1. Building efficient storage to find ancestors and descendants of transactions.
1. Frequently checking to ensure that blocks are valid, and reverting them if they are not. (An undiagnosed bug in my code kept packing invalid blocks, instead of fixing it I just ignored it since it was random.)
1. Using a genetic algorithm to find the optimal block. Initially I wrote my code to solve for a block deterministically -- swapping out transactions for clearly better transactions that saved fees. However my packing algorithm improved substantially once I randomally did the opposite behavior of what I expected was optimal, and when I generated 100 blocks per geneneration and kept the highest fee block (or kept the top 20%). Overal I was able to improve fees per block by 41% using this algorithm.
