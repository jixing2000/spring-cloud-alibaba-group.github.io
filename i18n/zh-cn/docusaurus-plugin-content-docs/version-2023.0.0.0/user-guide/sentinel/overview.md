---
title: 概述
keywords: [Spring Cloud Alibaba, Sentinel]
description: Sentinel, Overivew.
---

## 限流降级

在微服务系统中，一个对外的业务功能可能会涉及很长的服务调用链路。当其中某个服务出现异常，如果没有服务调用保护
机制可能会造成该服务调用链路上大量相关服务直接或间接调用的服务器仍然持续不断发起请求，最终导致相关的所有服务资源耗尽产生异常发生雪崩效应。限流和降级分别作为在流量控制和服务保护方面的两个重要手段，可以有效地应对此类问题。

### 限流

限流是一种针对服务提供者的策略，用于控制对特定服务接口或服务实例的访问量。其目的在于保护服务提供者免受过大请求流量的影响，确保服务稳定性。限流措施可以在服务提供者或服务消费者两端实现，通过设定流量阈值并采取排队、拒绝请求或返回错误信息等方式来控制流量，从而保护服务。

### 降级

降级是针对服务消费者的应对策略，在服务出现异常或限流时，通过对服务调用进行降级处理，确保消费者端能够在异常情况下正常工作。降级的目的在于转变为弱依赖状态，使系统能够在服务不可用时提供基本的功能或数据。这种策略可以在服务消费者端实施，通过返回默认值、提供备用数据或简化功能等方式来保证系统的可用性。

总体而言，限流和降级作为微服务架构中的重要机制，尽管在实现上可能有多种方式，但它们都着眼于保护服务提供者和消费者，在面对异常情况时确保系统稳定运行。限流关注于保护服务提供者，控制请求流量；而降级则关注于服务消费者，确保在服务不可用或异常情况下提供基本的功能。

## Sentinel 概述

Spring Cloud Alibaba 集成的开箱即用限流降级方案来自 [Sentinel](https://github.com/alibaba/Sentinel)，其以流量为切入点，从流量控制、熔断降级、系统负载保护等多个维度保护服务的稳定性。

Sentinel 具有以下特征:

- _丰富的应用场景_： Sentinel 承接了阿里巴巴近 10 年的双十一大促流量的核心场景，例如秒杀（即突发流量控制在系统容量可以承受的范围）、消息削峰填谷、实时熔断下游不可用应用等。
- _完备的实时监控_： Sentinel 同时提供实时的监控功能。您可以在控制台中看到接入应用的单台机器秒级数据，甚至 500 台以下规模的集群的汇总运行情况。
- _广泛的开源生态_： Sentinel 提供开箱即用的与其它开源框架/库的整合模块，例如与 Spring Cloud、Dubbo、gRPC 的整合。您只需要引入相应的依赖并进行简单的配置即可快速地接入 Sentinel。
- _完善的 SPI 扩展点_： Sentinel 提供简单易用、完善的 SPI 扩展点。您可以通过实现扩展点，快速的定制逻辑。例如定制规则管理、适配数据源等。