### Error over a Layer
$$\delta^{(L)} = a^{(L)} - y$$
### Error over the previous layer 
error for the layer $l-1$ propagated backwards from layer $l$
$$\delta^{(L-1)} = \left( W^{(L)} \right)^T \delta^{(L)} \cdot \sigma'(z^{(L-1)})$$
### Error of the current layer 
$$\delta^{(l)} = \left( W^{(l+1)} \right)^T \delta^{(l+1)} \cdot \sigma'(z^{(l)})$$
### Error WRT the weights of some neuron 
$$\frac{\partial L}{\partial W^{(l)}_{ij}} = \delta^{(l)}_j \cdot a^{(l-1)}_i$$
Where 
$$δ_j^{(l)}​=σ^{'}(zj(l)​)k∑​δ_k^{(l+1)}​W_{jk}^{(l+1)}$$
and 
$$\frac{\partial L}{\partial a^{(L)}} = a^{(L)} - y$$
$$\frac{\partial z^{(l)}_j}{\partial W^{(l)}_{ij}} = a^{(l-1)}_i$$

### Compact Form 
$$\delta^{(l)} = \left( W^{(l+1)} \right)^T \delta^{(l+1)} \cdot \sigma'(z^{(l)})$$
$$\frac{\partial L}{\partial W^{(l)}} = \delta^{(l)} \cdot \left( a^{(l-1)} \right)^T$$


# 
