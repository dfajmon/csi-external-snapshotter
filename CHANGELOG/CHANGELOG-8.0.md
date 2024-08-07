# Release notes for v8.0.1

[Documentation](https://kubernetes-csi.github.io)

## Changes by Kind

### Bug or Regression

- Update csi-lib-utils to v0.18.1 ([#1101](https://github.com/kubernetes-csi/external-snapshotter/pull/1101), [@solumath](https://github.com/solumath))

## Dependencies

### Added
_Nothing has changed._

### Changed
- github.com/kubernetes-csi/csi-lib-utils: [v0.18.0 → v0.18.1](https://github.com/kubernetes-csi/csi-lib-utils/compare/v0.18.0...v0.18.1)

### Removed
_Nothing has changed._

# Release notes for v8.0.0

[Documentation](https://kubernetes-csi.github.io)

# Changelog since v7.0.0

## Urgent Upgrade Notes

### (No, really, you MUST read this before you upgrade)

- The validating logic for VolumeSnapshots, VolumeSnapshotContents, VolumeGroupSnapshots, and
  VolumeGroupSnapshotContents has been replaced by CEL validation rules. The validating webhook
  is now only being used for VolumeSnapshotClasses and VolumeGroupSnapshotClasses to ensure
  that there's at most one class per CSI Driver. The validation webhook is deprecated and will be removed in the next release. ([#1091](https://github.com/kubernetes-csi/external-snapshotter/pull/1091), [@leonardoce](https://github.com/leonardoce))

## Changes by Kind

### API Change

- Update API for group snapshots, easing the restore process. ([#1068](https://github.com/kubernetes-csi/external-snapshotter/pull/1068), [@leonardoce](https://github.com/leonardoce))

### Feature

- Adds support for ListSnapshots secrets ([#252](https://github.com/kubernetes-csi/external-snapshotter/pull/252), [@bells17](https://github.com/bells17))
- Adds validation rules into CRDs. Minimum required Kubernetes version is 1.25 for these validation rules. ([#1073](https://github.com/kubernetes-csi/external-snapshotter/pull/1073), [@cici37](https://github.com/cici37))
- Link the snapshotted PVCs and the corresponding PVs in VolumeGroupSnapshot and VolumeGroupSnapshotContent to make restoring data easier. ([#1069](https://github.com/kubernetes-csi/external-snapshotter/pull/1069), [@leonardoce](https://github.com/leonardoce))
- Updated Kubernetes deps to v1.30 ([#1088](https://github.com/kubernetes-csi/external-snapshotter/pull/1088), [@jsafrane](https://github.com/jsafrane))

### Bug or Regression

- Adding the annotation `groupsnapshot.storage.kubernetes.io/is-default-class=true` on a VolumeGroupSnapshotClass will cause that VolumeGroupSnapshotClass to be used by default. ([#1015](https://github.com/kubernetes-csi/external-snapshotter/pull/1015), [@nixpanic](https://github.com/nixpanic))
- Fixed a bug in the csi-snapshotter sidecar causing it to rapidly make RPC calls to CSI drivers due to its own updates to VolumeSnapshotContent objects ([#1009](https://github.com/kubernetes-csi/external-snapshotter/pull/1009), [@ConnorJC3](https://github.com/ConnorJC3))
- Fixes a panic in the snapshot validation webhook. ([#1005](https://github.com/kubernetes-csi/external-snapshotter/pull/1005), [@xing-yang](https://github.com/xing-yang))
- Fixes a problem deleting VolumeSnapshotContent with `Retain` policy for pre-provisioned snapshots. ([#249](https://github.com/kubernetes-csi/external-snapshotter/pull/249), [@xing-yang](https://github.com/xing-yang))
- Prevent VolumeSnapshotContent's update from erroring out because of conflicts in the CSI snapshotter sidecar. ([#1066](https://github.com/kubernetes-csi/external-snapshotter/pull/1066), [@leonardoce](https://github.com/leonardoce))
- Prevent snapshot controller from panicking when requesting a VolumeGroupSnapshot of a non-CSI volume. ([#1067](https://github.com/kubernetes-csi/external-snapshotter/pull/1067), [@leonardoce](https://github.com/leonardoce))
- This change will update the Restore size in volumesnapshotcontent to the size it's received from the CSI driver. If `0` is received, it won't be added to the Restore size as it means it is unspecified as per CSI spec. ([#1011](https://github.com/kubernetes-csi/external-snapshotter/pull/1011), [@Madhu-1](https://github.com/Madhu-1))

### Other (Cleanup or Flake)

- Replace code-generator/generate-groups.sh with code-generator/kube_codegen.sh in update-generated-code.sh. ([#1075](https://github.com/kubernetes-csi/external-snapshotter/pull/1075), [@xing-yang](https://github.com/xing-yang))
- The Namespace additional printer column is now generated from a marker in the codebase instead of directly added in the CRD. ([#1094](https://github.com/kubernetes-csi/external-snapshotter/pull/1094), [@leonardoce](https://github.com/leonardoce))
- The validating logic for VolumeSnapshots, VolumeSnapshotContents, VolumeGroupSnapshots, and
  VolumeGroupSnapshotContents has been replaced by CEL validation rules. The validating webhook
  is now only being used for VolumeSnapshotClasses and VolumeGroupSnapshotClasses to ensure
  that there's at most one class per CSI Driver. ([#1091](https://github.com/kubernetes-csi/external-snapshotter/pull/1091), [@leonardoce](https://github.com/leonardoce))
- Update client to v8. ([#1093](https://github.com/kubernetes-csi/external-snapshotter/pull/1093), [@xing-yang](https://github.com/xing-yang))
- Updates Kubernetes 1.30 dependencies for the client and the server. ([#1071](https://github.com/kubernetes-csi/external-snapshotter/pull/1071), [@xing-yang](https://github.com/xing-yang))

### Uncategorized

- Adds secret reference to volume group snapshot content. ([#1034](https://github.com/kubernetes-csi/external-snapshotter/pull/1034), [@manishym](https://github.com/manishym))
- Fix bug in retrieving the group secret from the volumegroupsnapshotcontent object ([#1048](https://github.com/kubernetes-csi/external-snapshotter/pull/1048), [@Madhu-1](https://github.com/Madhu-1))
- Update google.golang.org/protobuf to v1.33.0 to resolve CVE-2024-24786 ([#1033](https://github.com/kubernetes-csi/external-snapshotter/pull/1033), [@dobsonj](https://github.com/dobsonj))
- Update manifests with controller-gen@v0.15.0 and new validation rules. Minimum required Kubernetes version is 1.25 for these validation rules. ([#1076](https://github.com/kubernetes-csi/external-snapshotter/pull/1076), [@xing-yang](https://github.com/xing-yang))
- Use Group secret for the GetGroupSnapshotStatus RPC call ([#1051](https://github.com/kubernetes-csi/external-snapshotter/pull/1051), [@Madhu-1](https://github.com/Madhu-1))

## Dependencies

### Added
- github.com/fxamacker/cbor/v2: [v2.6.0](https://github.com/fxamacker/cbor/v2/tree/v2.6.0)
- github.com/x448/float16: [v0.8.4](https://github.com/x448/float16/tree/v0.8.4)
- go.uber.org/goleak: v1.3.0
- k8s.io/gengo/v2: 51d4e06

### Changed
- cloud.google.com/go/compute/metadata: v0.2.3 → v0.3.0
- cloud.google.com/go/compute: v1.23.3 → v1.25.1
- github.com/cespare/xxhash/v2: [v2.2.0 → v2.3.0](https://github.com/cespare/xxhash/v2/compare/v2.2.0...v2.3.0)
- github.com/cncf/xds/go: [523115e → 8a4994d](https://github.com/cncf/xds/go/compare/523115e...8a4994d)
- github.com/emicklei/go-restful/v3: [v3.11.0 → v3.12.0](https://github.com/emicklei/go-restful/v3/compare/v3.11.0...v3.12.0)
- github.com/envoyproxy/go-control-plane: [v0.11.1 → v0.12.0](https://github.com/envoyproxy/go-control-plane/compare/v0.11.1...v0.12.0)
- github.com/envoyproxy/protoc-gen-validate: [v1.0.2 → v1.0.4](https://github.com/envoyproxy/protoc-gen-validate/compare/v1.0.2...v1.0.4)
- github.com/go-logr/zapr: [v1.2.3 → v1.3.0](https://github.com/go-logr/zapr/compare/v1.2.3...v1.3.0)
- github.com/go-openapi/jsonpointer: [v0.19.6 → v0.21.0](https://github.com/go-openapi/jsonpointer/compare/v0.19.6...v0.21.0)
- github.com/go-openapi/jsonreference: [v0.20.2 → v0.21.0](https://github.com/go-openapi/jsonreference/compare/v0.20.2...v0.21.0)
- github.com/go-openapi/swag: [v0.22.3 → v0.23.0](https://github.com/go-openapi/swag/compare/v0.22.3...v0.23.0)
- github.com/golang/glog: [v1.1.2 → v1.2.0](https://github.com/golang/glog/compare/v1.1.2...v1.2.0)
- github.com/golang/protobuf: [v1.5.3 → v1.5.4](https://github.com/golang/protobuf/compare/v1.5.3...v1.5.4)
- github.com/google/uuid: [v1.4.0 → v1.6.0](https://github.com/google/uuid/compare/v1.4.0...v1.6.0)
- github.com/kubernetes-csi/csi-lib-utils: [v0.17.0 → v0.18.0](https://github.com/kubernetes-csi/csi-lib-utils/compare/v0.17.0...v0.18.0)
- github.com/onsi/ginkgo/v2: [v2.13.1 → v2.15.0](https://github.com/onsi/ginkgo/v2/compare/v2.13.1...v2.15.0)
- github.com/onsi/gomega: [v1.30.0 → v1.31.0](https://github.com/onsi/gomega/compare/v1.30.0...v1.31.0)
- github.com/prometheus/client_golang: [v1.18.0 → v1.19.1](https://github.com/prometheus/client_golang/compare/v1.18.0...v1.19.1)
- github.com/prometheus/client_model: [v0.5.0 → v0.6.1](https://github.com/prometheus/client_model/compare/v0.5.0...v0.6.1)
- github.com/prometheus/common: [v0.46.0 → v0.53.0](https://github.com/prometheus/common/compare/v0.46.0...v0.53.0)
- github.com/prometheus/procfs: [v0.12.0 → v0.15.0](https://github.com/prometheus/procfs/compare/v0.12.0...v0.15.0)
- github.com/rogpeppe/go-internal: [v1.10.0 → v1.11.0](https://github.com/rogpeppe/go-internal/compare/v1.10.0...v1.11.0)
- github.com/stretchr/objx: [v0.5.0 → v0.1.0](https://github.com/stretchr/objx/compare/v0.5.0...v0.1.0)
- github.com/stretchr/testify: [v1.8.4 → v1.9.0](https://github.com/stretchr/testify/compare/v1.8.4...v1.9.0)
- github.com/yuin/goldmark: [v1.4.13 → v1.3.5](https://github.com/yuin/goldmark/compare/v1.4.13...v1.3.5)
- go.opentelemetry.io/contrib/instrumentation/google.golang.org/grpc/otelgrpc: v0.46.0 → v0.51.0
- go.opentelemetry.io/otel/metric: v1.20.0 → v1.26.0
- go.opentelemetry.io/otel/trace: v1.20.0 → v1.26.0
- go.opentelemetry.io/otel: v1.20.0 → v1.26.0
- go.uber.org/zap: v1.19.0 → v1.26.0
- golang.org/x/crypto: v0.18.0 → v0.23.0
- golang.org/x/mod: v0.12.0 → v0.15.0
- golang.org/x/net: v0.20.0 → v0.25.0
- golang.org/x/oauth2: v0.16.0 → v0.20.0
- golang.org/x/sync: v0.5.0 → v0.7.0
- golang.org/x/sys: v0.16.0 → v0.20.0
- golang.org/x/term: v0.16.0 → v0.20.0
- golang.org/x/text: v0.14.0 → v0.15.0
- golang.org/x/time: v0.3.0 → v0.5.0
- golang.org/x/tools: v0.14.0 → v0.18.0
- google.golang.org/genproto/googleapis/api: bbf56f3 → 94a12d6
- google.golang.org/genproto/googleapis/rpc: bbf56f3 → 94a12d6
- google.golang.org/grpc: v1.61.0 → v1.64.0
- google.golang.org/protobuf: v1.32.0 → v1.34.1
- k8s.io/api: v0.29.0 → v0.30.0
- k8s.io/apimachinery: v0.29.0 → v0.30.0
- k8s.io/client-go: v0.29.0 → v0.30.0
- k8s.io/code-generator: v0.29.0 → v0.30.0
- k8s.io/component-base: v0.29.0 → v0.30.0
- k8s.io/component-helpers: v0.29.0 → v0.30.0
- k8s.io/kube-openapi: 2dd684a → 70dd376
- sigs.k8s.io/yaml: v1.3.0 → v1.4.0

### Removed
- github.com/cncf/udpa/go: [c52dc94](https://github.com/cncf/udpa/go/tree/c52dc94)
- github.com/creack/pty: [v1.1.9](https://github.com/creack/pty/tree/v1.1.9)
- github.com/kr/pty: [v1.1.1](https://github.com/kr/pty/tree/v1.1.1)
- github.com/matttproud/golang_protobuf_extensions/v2: [v2.0.0](https://github.com/matttproud/golang_protobuf_extensions/v2/tree/v2.0.0)
- go.uber.org/atomic: v1.10.0
- google.golang.org/genproto: bbf56f3
- k8s.io/gengo: 9cce18d
