# Kaldi-Debugging

## Errors

1. `compute-mfcc-feats` command not found: 
    1. In `run.sh`, it calls `$KALDI_ROOT/tools/config/common_path.sh`. It should do `export PATH=$KALDI_ROOT/src/featbin` etc. but it doesn't happen. So, do it separately on your terminal.

	```shell
	export KALDI_ROOT=/home/wireless/Documents/kaldi
	export PATH=$KALDI_ROOT/src/featbin:$PATH
	```
2. `qsub: command not found` (This comes when using queue.pl file):
    1. `qsub` is used for parallelization, to allow using multiple systems at a time. To use everything on a single system only, open `cmd.sh` and set `export train_cmd="run.pl"`. That's it.
3. Below is a warning, freely ignore. It should work, after a few passes. If it doesn't, check where `queue.pl` is being called.
  ```sh
  queue.pl: Error submitting jobs to queue (return status was 256)
queue log file is exp/mono/decode_nosp_tgsmall_dev_clean_2/q/decode.log, command was qsub -v PATH -cwd -S /bin/bash -j y -l arch=*64* -o exp/mono/decode_nosp_tgsmall_dev_clean_2/q/decode.log   -l mem_free=4G,ram_free=4G  -t 1:10 /home/wireless/Documents/kaldi/egs/mini_librispeech/s5/exp/mono/decode_nosp_tgsmall_dev_clean_2/q/decode.sh >>exp/mono/decode_nosp_tgsmall_dev_clean_2/q/decode.log 2>&1
  ```
