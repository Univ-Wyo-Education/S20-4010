
all:
	go build

sign1: 
	./sig-test sign-message UTC--2019-04-03T02-41-35.103996908Z--6E11C0aC0d8fEa2B53D70b32f9b01077a4B66A59 "some data to sign"

sign2: 
	echo Password Is: 78S2tAIfk4VP2xv2
	./sig-test sign-message UTC--2018-08-27T00-03-50.008098186Z--7e3aFEc048bC7be745d0fA0F5af97D3978C40E9A "some data to sign"

verify1:
	./sig-test verify-message 6E11C0aC0d8fEa2B53D70b32f9b01077a4B66A59 797a53a6886c5e0cd8e69e3ce43a041db49b86a403dcb3f751829eecd0cd48a41a41a7412cc61d58284bcec191ab4061e6f3de0a28fd71433da5367fac793d7e00 "some data to sign"

verify2:
	./sig-test verify-message 6E11C0aC0d8fEa2B53D70b32f9b01077a4B66A59 797a53a6886c5e0cd8e69e3ce43a041db49b86a403dcb3f751829eecd0cd48a41a41a7412cc61d58284bcec191ab4061e6f3de0a28fd71433da5367fac793d7e00 736f6d65206461746120746f207369676e
