输入
一个正在路上行走的银行家说，这个行当不行。

Tacotron2_gflin_48k.wav
Tacotron2+gflin+48k
训练Tacotron2时，mel是经过归一化的，归一化的mean和std是整个数据集的mean和std
训练Tacotron2时，没有大辞典，仅仅用了单个字的发音
暂且将该Tacotron2模型定为：Tacotron2_v1


Tacotron2_WaveRNN_48k.wav
Tacotron2+WaveRNN+48k
训练Tacotron2时，使用大辞典
WaveRNN时RAW模式训练的，训练WaveRNN时，mel没有经过归一化，所以在这里推理时，输入WaveRNN的mel特征（也就是上面的Tacotron2_v1模型输出的值）是已经经过反归一化的了。
在这里将该WaveRNN模型定为：WaveRNN_v1.1（WaveRNN_v1为MOL模式下训练的，效果不理想，几乎不能用）


Tacotron2_gflin_16k.wav
Tacotron2+gflin+16k
训练Tacotron2时，使用大辞典
训练Tacotron2时，mel是经过另外一个归一化程序的https://github.com/lturing/tacotronv2_wavernn_chinese/blob/master/tacotron/datasets/audio.py
暂且将该Tacotron2模型定为：Tacotron2_v2

Tacotron2_HiFiGan_16k.wav
Tacotron2+HifiGAN+16k
训练Tacotron2时，使用大辞典
训练Tacotron2时，feature的归一化还是跟最初的归一化方式类似，归一化的mean和std是整个数据集的mean和std，在使用librosa.feature.melspectrogram函数时，center=False，pad_mode='reflect'
训练HifgGan时，feature和音频的处理都需要与Tacotron2一致，在这个版本中，还有使用Tacotron2生成的数据对该HifiGan进行微调。
暂且将该该模型定为:Tacotron2_v2.1 + HifiGAN_v1

Tacotron2_HiFiGan_v1.1_16k.wav
与Tacotron2_HiFiGan_16k.wav类似，不同的是，改HiFiGan模型是经过基于Tacotron2生成的数据进行微调后的模型。
暂且将该该模型定为:Tacotron2_v2.1 + HifiGAN_v1.1

##到这里似乎可以做个简单的总结：
目前还是推荐使用Tacotron2+HifiGAN的组合，WaveRNN效果相对差，并且不稳定，容易跑飞，而且目前看HifiGAN不需要使用Tacotron2生成的数据进行finetune也能有较好的效果。另外，虽然单从这条音频看，HifiGan微调与否影响不大，但是从其他的整体结果看，FineTune后的HifiGan模型还是要比不Finetune的好一些。所以建议还是要Finetune。




