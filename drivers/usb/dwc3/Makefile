ccflags-$(CONFIG_USB_DWC3_DEBUG)	:= -DDEBUG
ccflags-$(CONFIG_USB_DWC3_VERBOSE)	+= -DVERBOSE_DEBUG
ccflags-y += -Idrivers/usb/host
ccflags-y += -Idrivers/base/power

obj-$(CONFIG_USB_DWC3)			+= dwc3.o

dwc3-y					:= core.o

ifneq ($(filter y,$(CONFIG_USB_DWC3_HOST) $(CONFIG_USB_DWC3_DUAL_ROLE)),)
	dwc3-y				+= host.o
endif

ifneq ($(filter y,$(CONFIG_USB_DWC3_GADGET) $(CONFIG_USB_DWC3_DUAL_ROLE)),)
	dwc3-y				+= gadget.o ep0.o
endif

dwc3-y					+= dwc3_otg.o

ifneq ($(CONFIG_DEBUG_FS),)
	dwc3-y				+= debugfs.o
endif

##
# Platform-specific glue layers go here
#
# NOTICE: Make sure your glue layer doesn't depend on anything
# which is arch-specific and that it compiles on all situations.
#
# We want to keep this requirement in order to be able to compile
# the entire driver (with all its glue layers) on several architectures
# and make sure it compiles fine. This will also help with allmodconfig
# and allyesconfig builds.
#
# The only exception is the PCI glue layer, but that's only because
# PCI doesn't provide nops if CONFIG_PCI isn't enabled.
##

obj-$(CONFIG_USB_DWC3)		+= dwc3-omap.o
#obj-$(CONFIG_USB_DWC3)		+= dwc3-exynos.o
obj-$(CONFIG_USB_DWC3_MSM)	+= dbm-1_4.o dbm-1_5.o dwc3-msm.o dbm.o

ifneq ($(CONFIG_PCI),)
	obj-$(CONFIG_USB_DWC3)		+= dwc3-pci.o
endif

