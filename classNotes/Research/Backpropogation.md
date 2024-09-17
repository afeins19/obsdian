$$\delta^{(L)} = a^{(L)} - y$$
$$\delta^{(L-1)} = \left( W^{(L)} \right)^T \delta^{(L)} \cdot \sigma'(z^{(L-1)})$$
$$\delta^{(l)} = \left( W^{(l+1)} \right)^T \delta^{(l+1)} \cdot \sigma'(z^{(l)})$$
$$\frac{\partial L}{\partial W^{(l)}_{ij}} = \delta^{(l)}_j \cdot a^{(l-1)}_i$$
$$\frac{\partial L}{\partial a^{(L)}} = a^{(L)} - y$$
$$\frac{\partial z^{(l)}_j}{\partial W^{(l)}_{ij}} = a^{(l-1)}_i$$

### Compact Form 
$$\delta^{(l)} = \left( W^{(l+1)} \right)^T \delta^{(l+1)} \cdot \sigma'(z^{(l)})$$
$$\frac{\partial L}{\partial W^{(l)}} = \delta^{(l)} \cdot \left( a^{(l-1)} \right)^T$$
