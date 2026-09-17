# 200G-Ethernet-PMA
My goal is to build a complete 200G Ethernet PMA VIP from the Ethernet specification and its verification using UVM.
- PMA RTL/model
- UVM verification environment
- standalone PMA verification
- functional + assertion + code coverage


The 200GBASE-R PMA(s) can support any of the 200 Gb/s PMDs in Table 116–1

<img width="732" height="417" alt="image" src="https://github.com/user-attachments/assets/5aa61c82-d925-4876-a664-d345057266e4" />

The principal functions implemented (when required) by the PMA in both the transmit and receive directions:
1. Adapt the PCSL formatted signal to the appropriate number of abstract or physical lanes.
2. Provide per input-lane clock and data recovery.
3. Provide bit-level multiplexing.
4. Provide clock generation.
5. Provide signal drivers.
6. Optionally provide local loopback to/from the PMA service interface.
7. Optionally provide remote loopback to/from the PMD service interface.
8. Optionally provide test-pattern generation and detection.
9. Tolerate Skew Variation.
10. Perform PAM4 encoding and decoding for 200GBASE-R PMAs where the number of physical lanes is 4.

In addition, the PMA provides receive link status information in the receive direction.

### **PMA sublayer positioning**

The number of input lanes and the number of output lanes for a PMA are always divisors of the number of PCSLs. For PMA sublayers supporting 200GBASE-R PMDs, the number of PCSLs is 8.

<img width="719" height="548" alt="image" src="https://github.com/user-attachments/assets/e141a576-11db-4bfa-8719-f7d770323653" />

The following guidelines apply to the partitioning of PMAs:
1. The inter-sublayer service interface, defined in 116.3.1, is used for the PMA service interfaces
supporting a flexible architecture with multiple PMA sublayers.
- An instance of this interface can only connect service interfaces with the same number of lanes,
where the lanes operate at the same rate.
2. 200GAUI-n is a physical instantiation of the connection between two adjacent 200GBASE-R PMA
sublayers with the exception of the inst:IS_SIGNAL.indication which is carried outside of this
physically instantiated interface. 400GAUI-n is a physical instantiation of the connection between
two adjacent 400GBASE-R PMA sublayers with the exception of the inst:IS_SIGNAL.indication
which is carried outside of this physically instantiated interface.
- As physical instantiations, these define electrical and timing specification as well as requiring a
receive re-timing function.
- 200GAUI-8 is a 26.5625 GBd by 8 lane NRZ physical instantiation of the 200 Gb/s
connection. 400GAUI-16 is a 26.5625 GBd by 16 lane NRZ physical instantiation of the
400 Gb/s connection.
- 200GAUI-4 is a 26.5625 GBd by 4 lane PAM4 physical instantiation of the 200 Gb/s
connection. 400GAUI-8 is a 26.5625 GBd by 8 lane PAM4 physical instantiation of the
400 Gb/s connection.
3. The abstract inter-sublayer service interface can be physically instantiated as a 200GAUI-n or
400GAUI-n, using associated PMAs to map to the appropriate number of lanes.
4. Opportunities for optional test-pattern generation, optional test-pattern detection, optional local
loopback and optional remote loopback are dependent upon the location of the PMA sublayer in the
implementation. See Figure 120–5.
5. A minimum of one PMA sublayer is required in a PHY.
6. A maximum of four PMA sublayers are addressable as MDIO MMDs.



The PMA bit mux operates in one direction of transmission by demultiplexing PCSLs from m PMA input lanes and remultiplexing them into n PMA output lanes. The mapping of PCSLs from input to output lanes is not specified.
The parameters of a PMA include the following:
- The numbers of input and output lanes in each direction.
- Whether the PMA is adjacent to a physically instantiated interface (200GAUI-n or 400GAUI-n above or below).
- Whether the PMA is adjacent to the PCS or DTE XS.
- Whether the PMA is adjacent to the PMD or PHY XS.

<img width="941" height="829" alt="image" src="https://github.com/user-attachments/assets/d892e894-d84f-4785-a784-6403478e079f" />
