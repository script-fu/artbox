---
type: docs
url: "hub/feature-test/folder/System-Performance"
---

# System Performance

CPU-aware, user-configuration-based performance optimization with intelligent profiles that automatically configure memory allocation, tile sizes, and threading parameters.

## Performance Profiles

{{< cards >}}
  {{< card link="#conservative-profile" title="Conservative Profile" subtitle="2GB RAM, 2 cores - Safe defaults for limited systems" icon="one" >}}
  {{< card link="#balanced-profile" title="Balanced Profile" subtitle="8GB RAM, 4 cores - Optimal for most users" icon="cards" >}}
  {{< card link="#high-profile" title="High Performance" subtitle="16GB RAM, 8 cores - Enhanced processing power" icon="warning" >}}
  {{< card link="#extreme-profile" title="Extreme Profile" subtitle="32GB RAM, 12 cores - Professional workstations" icon="warning" >}}
  {{< card link="#ultra-profile" title="Ultra Profile" subtitle="64GB RAM, 20 cores - High-end systems" icon="warning" >}}
  {{< card link="#maximum-profile" title="Maximum Profile" subtitle="128GB+ RAM, 32+ cores - Workstation class" icon="warning" >}}
{{< /cards >}}

## Core Optimizations

{{< cards >}}
  {{< card link="#cpu-aware-threading" title="CPU-Aware Threading" subtitle="Intelligent pixels-per-thread calculation based on configured cores" icon="cards" >}}
  {{< card link="#cache-aware-tiles" title="Cache-Aware Tile Sizing" subtitle="Adaptive tile sizes optimized for user's cache allocation" icon="copy" >}}
  {{< card link="#plugin-optimization" title="Plugin Optimization" subtitle="Configurable external plugin tile sizes for better data transfer" icon="folder-tree" >}}
  {{< card link="#gegl-integration" title="GEGL Integration" subtitle="Direct wiring of performance settings into GEGL's core systems" icon="cards" >}}
{{< /cards >}}

---

<div class="feature-section" id="conservative-profile">

## Conservative Profile

**Target System**: 2GB RAM, 2 cores

**Current State**: Hardcoded performance values that don't adapt to system capabilities.

**Solution**: Safety-first profile with conservative memory allocation and threading parameters.

**Configuration**:
- **Tile Cache**: 1GB - Minimal RAM allocation before disk swapping
- **Undo Memory**: 512MB - Limited undo history storage  
- **Threading**: MAX(optimal, 8192) pixels per thread - Prioritizes stability
- **Tile Sizes**: MIN(optimal, 256) - Memory-conservative tile dimensions
- **Plugin Tiles**: 128x128 - Small data transfer packets

**Benefits**: Stable operation on older or resource-limited systems.

</div>

---

<div class="feature-section" id="balanced-profile">

## Balanced Profile

**Target System**: 8GB RAM, 4 cores

**Current State**: Default GIMP settings often suboptimal for modern mid-range systems.

**Solution**: Mathematically optimized settings based on GEGL's parallel distribution algorithm.

**Configuration**:
- **Tile Cache**: 4GB - Balanced RAM usage for smooth operation
- **Undo Memory**: 2GB - Adequate undo history storage
- **Threading**: Pure CPU optimization - Calculated optimal pixels per thread
- **Tile Sizes**: Cache-optimized dimensions
- **Plugin Tiles**: Adaptive sizing based on cache configuration

**Benefits**: Balanced performance for modern mid-range systems.

</div>

---

<div class="feature-section" id="high-profile">

## High Performance Profile

**Target System**: 16GB RAM, 8 cores

**Current State**: GIMP defaults leave high-end consumer systems underutilized.

**Solution**: Aggressive performance tuning with enhanced memory allocation.

**Configuration**:
- **Tile Cache**: 8GB - Large cache for complex operations
- **Undo Memory**: 4GB - Extended undo capabilities
- **Threading**: MIN(optimal, 32768) pixels per thread - Aggressive parallelization
- **Tile Sizes**: MAX(optimal, 512) - Performance-optimized tiles
- **Plugin Tiles**: Large adaptive tiles for faster data transfer

**Benefits**: Enhanced performance on high-end consumer and prosumer systems.

</div>

---

<div class="feature-section" id="extreme-profile">

## Extreme Profile

**Target System**: 32GB RAM, 12 cores

**Current State**: Professional workstations constrained by conservative defaults.

**Solution**: Very aggressive optimization for professional workflows.

**Configuration**:
- **Tile Cache**: 22.5GB - Massive cache for professional workloads
- **Undo Memory**: 4GB - Professional-grade undo storage
- **Threading**: MIN(optimal, 16384) pixels per thread - Very aggressive threading
- **Tile Sizes**: 1024x1024 - Maximum tile dimensions
- **Plugin Tiles**: Maximum size for optimal throughput

**Benefits**: Improved performance for professional workstation hardware.

</div>

---

<div class="feature-section" id="ultra-profile">

## Ultra Profile

**Target System**: 64GB RAM, 20 cores

**Current State**: High-end workstations severely limited by default settings.

**Solution**: Maximum performance optimization for demanding professional use.

**Configuration**:
- **Tile Cache**: 56GB - Enormous cache for complex professional projects
- **Undo Memory**: 4GB - Maintained professional undo levels
- **Threading**: Pure optimization - Calculated for maximum efficiency
- **Tile Sizes**: 1024x1024 - Maximum performance tiles
- **Plugin Tiles**: Optimized for high-throughput workflows

**Benefits**: High performance for high-end professional and scientific workstations.

</div>

---

<div class="feature-section" id="maximum-profile">

## Maximum Profile

**Target System**: 128GB+ RAM, 32+ cores

**Current State**: Enterprise-class systems hobbled by conservative assumptions.

**Solution**: Ultra-aggressive optimization for maximum hardware utilization.

**Configuration**:
- **Tile Cache**: 120GB - Enterprise-scale memory allocation
- **Undo Memory**: 4GB - Maintained for stability
- **Threading**: MAX(optimal/2, 2048) pixels per thread - Ultra-aggressive threading
- **Tile Sizes**: 1024x1024 - Maximum tile dimensions
- **Plugin Tiles**: Maximum throughput configuration

**Benefits**: High utilization of enterprise-class hardware.

</div>

---

<div class="feature-section" id="cpu-aware-threading">

## CPU-Aware Threading

**Current State**: Fixed pixels-per-thread values (4096) regardless of CPU configuration.

**Issue**: Threading parameters don't adapt to configured core count. Benefits are mainly visible for small to medium-sized operations where thread distribution matters.

**Solution**: Adaptive calculation of pixels-per-thread based on configured thread count using GEGL's parallel distribution algorithm.

**Technical Implementation**:

- Uses `gegl_config->num_processors` (user's thread setting) rather than hardware detection
- Applies GEGL formula: `n_threads = floor((c + sqrt(c * (c + 4.0 * n))) / (2.0 * c))`
- Algorithm: 2 cores→32768, 4 cores→16384, 8 cores→8192, 8+ cores→4096 pixels per thread
- Balances thread coordination overhead against parallelism

**Performance Impact**:

- **Large operations (10k×10k images)**: Minimal benefit - most settings achieve full CPU utilization
- **Medium operations (2k×2k regions)**: Moderate improvement for multi-core systems  
- **Small operations (512×512 selections)**: Significant improvement - can utilize more cores effectively

**Benefits**: Better thread utilization for small to medium operations, respects user's thread configuration.

</div>

---

<div class="feature-section" id="cache-aware-tiles">

## Cache-Aware Tile Sizing

**Current State**: Hardcoded tile sizes that ignore user's memory allocation.

**Issue**: Tile dimensions don't scale with available cache, missing potential optimization opportunities.

**Solution**: Adaptive tile sizing based on user's configured tile cache size.

**Technical Implementation**:

- Uses `gegl_config->tile_cache_size` (user's cache setting) for calculations
- Larger caches receive larger tiles for better memory efficiency
- Applied to both GEGL internal tiles and external plugin communication
- Respects user's actual memory allocation decisions

**Benefits**: Improved cache utilization and memory access patterns aligned with user's configuration.

</div>

---

<div class="feature-section" id="plugin-optimization">

## Plugin Optimization

**Current State**: Fixed 128x128 plugin tile sizes regardless of system capabilities.

**Issue**: External plugin communication uses conservative tile sizes that may limit data transfer efficiency.

**Solution**: Configurable plugin tile dimensions that adapt to system performance profile.

**Technical Implementation**:

- Exposes `plugin-tile-width` and `plugin-tile-height` properties
- Automatically sized based on user's cache configuration and performance profile
- Applied to Script-Fu, Python-Fu, and all external plugin communication
- Affects memory allocation per transfer: `tile_width × tile_height × bytes_per_pixel`

**Benefits**: Improved data transfer efficiency between Artbox core and external plugins.

</div>

---

<div class="feature-section" id="gegl-integration">

## GEGL Integration

**Current State**: Performance settings applied inconsistently across GEGL operations.

**Issue**: Core image processing operations don't benefit from user's performance configuration.

**Solution**: Direct integration of performance settings into GEGL's initialization and operation systems.

**Technical Implementation**:

- Settings applied once at startup (restart required for changes)
- Global variables initialized for consistent use across all GEGL operations
- Tile cache size directly mapped to `gegl_config()->tile-cache-size`
- Thread count directly mapped to `gegl_config()->threads`
- Pixels-per-thread used in all parallel processing operations

**Benefits**: Consistent performance optimization across all image processing operations with proper integration into GEGL's core systems.

</div>

---
